---
layout: post
title:  "자바 성능 튜닝 이야기 - 9장 (IO 관련)"
date:   2021-01-26
last_modified_at: 2021-01-26
categories: [book, JAVA, TUNNING]
tags: [book, JAVA, TUNNING]
---

**IO 처리**
- BufferedReader > 버퍼 포함한 FileReader > 버퍼 없이 FileRader 속도 순으로 빠르다.
- DirectByteBuffer를 사용할 때 주의해야한다. ByteBuffer 객체를 생성하는 메서드 중 allocateDirect()가 있는데 OS 메모리에 할당된 메모리를 Native한 JNI로 처리하는 DirectByteBuffer 객체를 생성한다. DirectByteBuffer 생성자는 java.nio에 아무런 접근 제어자가 없이 선언된 Bits라는 클래스의 reverseMemory() 메서드를 호출하고 이 메서드는 JVM에 할당되어 있는 메모리보다 더 많은 메모리를 요구할 경우 System.gc() 메서드를 호출하도록 되어있다. singleton 패턴을 사용하여 해당 JVM에는 하나의 객체만 생성하도록 권장한다.
- lastModified() 대신 WatchService를 사용하는 실습
```java
public class WatchSample {
	public static void main(String[] args) {
		WatcherThread thread = new WatcherThread("C:\\Temp");
		thread.start();
	}
}
```

```java
import java.nio.file.FileSystems;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.WatchEvent;
import java.nio.file.WatchKey;
import java.nio.file.WatchService;
import java.util.Date;
import java.util.List;

import static java.nio.file.StandardWatchEventKinds.ENTRY_CREATE;
import static java.nio.file.StandardWatchEventKinds.ENTRY_DELETE;
import static java.nio.file.StandardWatchEventKinds.ENTRY_MODIFY;

public class WatcherThread extends Thread{
	String dirName;
	public WatcherThread(String dirName) {
		this.dirName=dirName;
	}
	public void run() {
		System.out.print("Watcher is started");
		fileWatcher();
		System.out.println("Watcher is ended");
	}
	public void fileWatcher() {
		try {
			Path dir = Paths.get(dirName);
			WatchService watcher = FileSystems.getDefault().newWatchService();
			dir.register(watcher, ENTRY_CREATE, ENTRY_DELETE, ENTRY_MODIFY);
			
			WatchKey key;
			for(int loop=0; loop<4; loop++) {
				key = watcher.take();
				String watchedTime = new Date().toString();
				List<WatchEvent<?>> eventList = key.pollEvents();
				for(WatchEvent<?> event : eventList) {
					Path name = (Path) event.context();
					if(event.kind() == ENTRY_CREATE) {
						System.out.format("%s created at %s%n", name, watchedTime);
					} else if(event.kind() == ENTRY_DELETE) {
						System.out.format("%s deleted at %s%n", name, watchedTime);
					} else if(event.kind() == ENTRY_MODIFY) {
						System.out.format("%s modified at %s%n", name, watchedTime);
					}
				}
				key.reset();
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

<br/>

출처 : 자바 성능 튜닝 이야기 이상민 지음

<br/>