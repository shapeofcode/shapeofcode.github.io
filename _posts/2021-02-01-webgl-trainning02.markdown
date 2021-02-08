---
layout: post
title:  "WebGL - GLSL/Shader(1)"
date:   2021-02-01
last_modified_at: 2021-02-01
categories: [3D]
tags: [webgl]
---
**GLSL (OpenGL Shading Language)**

- 데이터 타입 : float, int, bool, vec2(f,f), vec3(f,f,f), vec4(f,f,f,f) - rgba ...
- GLSL은 타입에 엄격하다. (. 때문에 컴파일이 안되기도 함)

<br/>

**uniform**
cpu에서 gpu로 정보를 넘겨주는 변수

<br/>

**gl_FragCoord**
픽셀의 위치 정보 (좌측 하단을 원점으로 시작)

<br/>

**smoothstep**
두 값 사이의 보간 수행

ex) vec2 smoothstep(float edge0, float edge1, vec2 x)
```javascript
uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

// Plot a line on Y using a value between 0.0-1.0
float plot(vec2 st) {
    // y와 x     
    return smoothstep(0.020, 0.0, abs(st.y - st.x));
}

void main() {
	vec2 st = gl_FragCoord.xy/u_resolution;

    float y = st.x;

    vec3 color = vec3(y);

    // Plot a line
    float pct = plot(st);
    color = (1.0-pct)*color+pct*vec3(0.0,1.0,0.0);

	gl_FragColor = vec4(color,1.0);
}
```

<br/>

**내장함수**

- pow(st.x,5.0) x의 5승
- step(0.5,st.x) 0.5를 기준으로 x 가 0.5 보다 작으면 0 크면 1
- sin(x) sin 주기
- con(x) cos 주기
- mod(x,1.5) 나머지 연산
- fract(x) 소숫점만 리턴
- ceil(x) 올림
- floor(x) 내림
- sign(x) 양수 1리턴 음수 -1 리턴
- abs(x) 절대값 리턴
- clamp(x,0.0,1.0) 리턴값을 지정된 범위로 지정
- min(0.0,x) 둘중 작은 변수 리턴
- max(0.0,x) 둘중 큰 변수 리턴
- gain(st.x, 1.5) smoothstep에서 기울기를 변화하는것

<br/>

출처 

[https://thebookofshaders.com/](https://thebookofshaders.com/)
[https://opentutorials.org/module/3659/21954](https://opentutorials.org/module/3659/21954)
[https://kblog.popekim.com/2011/11/01-part-1.html](https://kblog.popekim.com/2011/11/01-part-1.html)
<br/>
