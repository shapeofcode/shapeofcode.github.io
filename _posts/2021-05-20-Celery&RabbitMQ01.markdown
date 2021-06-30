---
layout: post
title:  "HackerRank - Celery & RabbitMQ (1)"
date:   2021-05-20
last_modified_at: 2021-05-20
categories: [Asynchronous]
tags: [Asynchronous]
---

<br/>

웹으로 프로그램을 구현할때에는 대게 모든 response는 네트워크가 빠르다는 가정하에 
1초 안에 떨어져야 한다고 생각한다. 
사용자의 편의성과 사이트에 머무는 시간은 그만큼 중요하기 때문이다. 
가끔 이러한 응답시간을 해결하기 위해 정적 리소스의 배치나 로딩바를 이용하거나 
비동기를 사용하여 처리하는 경우가 많다. 
때로는 사용자의 요청이 무거운 로직을 돌리는 (절대적인 시간이 필요한) 경우에는 
백그라운드 프로세스로 돌리고 이에대한 진행 사항을 웹 UI로 보여줌으로써 사용자가 
자신이 요청한 내용이 잘 동작하고 있구나 하는 인식을 심어주고 추후에 결과값이 
완료가 되면 최종 응답 메세지를 보내어 로직을 처리하는 방법이 있다.

<br/>

이를 위해 사용한 것이 Celery와 RabbitMQ이다.

<br/>

빠른 이해를 위해 먼저 작성된 블로그 글들 몇개를 훑어보고 공식문서를 살펴보았다.

<br/>

### Celery란?

셀러리는 파이썬으로 작성된 비동기 작업 큐 이다.


- 메세지를 통해 소통하며 브로커를 사용하여 클라이언트와 워커사이 중재한다.
- 클라이트가 작업을 큐에 담으면 브로커는 메세지를 워커에게 전달한다.
- 셀러리 시스템은 다수의 워커와 브로커로 구성될 수 있으며 수평적인 스케일링이 가능하다.

<br/>

##### 브로커 설치

여기서 말하는 브로커(메시지 전송자)는 여러가지가 있다. 
RabbitMQ, Redis, Amazon SQS 등등…
Celery에서 RabbitMQ는 안정적이고, 쉽고 지속가능하다고 소개한다.

<br/>

RabbitMQ는 윈도우, 도커, 리눅스 환경 등 다양한 환경에서 설치할 수 있다.

[RabbitMQ 설치법](https://www.rabbitmq.com/download.html)

<br/>

##### 셀러리 설치

파이썬 패키지 이므로

```
Pip install celery
```

<br/>

##### 사용법

처음에는 celery 객체가 필요하다. 이를 celery application이라고 부른다. 이 객체는
셀러리에서 하는 모든것의 진입점이 된다.(작업 생성, 워커 관리)

<br/>

1. Task.py 파일 작성

```
from celery import Celery
app = Celery('tasks', broker='pyamqp://guest@localhost//')
@app.task
def add(x, y):
    return x + y
```

<br/>

Celery 첫번째 인자 'tasks'는 현재 모듈의 이름이다. 
__main__모듈에서 작업이 정의될 때
자동으로 생성된다. 두번째 인자는 메시지 브로커 url이다.

<br/>

2. 셀러리 워커 서버 실행

이제 워커 변수를 통해 워커를 실행할 수 있다.

```
celery -A tasks worker --loglevel=INFO
```

<br/>

3. 작업 콜

delay() 함수를 통해 작업을 부를 수 있다.

```text
>>> from tasks import add
>>> add.delay(4, 4)
```

<br/>

task는  AsyncResult를 반환한다. 
이걸로 task의 상태를 체크하고 끝나기를 기다리거나
return value를 얻을 수 있다.

<br/>

4. 결과값을 유지하는 법

task의 상태를 계속 갖고 있을 필요가 있으면 여러 백앤드 요소를 사용할 수 있다.
(SQLAlchemy/Django ORM, MongoDB, Memcached, Redis, RPC (RabbitMQ/AMQP))

app = Celery('tasks', backend='rpc://', broker='pyamqp://')

```text
>>> result.ready()
```

<br/>

Ready 함수는 task processing이 끝났는지 알려준다.

<br/>

5. 설정

Rate limit 설정법

10개의 task만 1분안에 처리되도록 설정

```text
task_annotations = {
'tasks.add': {'rate_limit': '10/m'}
}

또는

celery -A tasks control rate_limit tasks.add 10/m
```

출처

[셀러리 doc](https://docs.celeryproject.org/en/stable/getting-started/first-steps-with-celery.html)
[셀러리 github](https://github.com/celery/celery)