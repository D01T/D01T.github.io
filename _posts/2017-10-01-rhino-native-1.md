---
title: "Rhino 자바스크립트 엔진에서 Native 라이브러리 사용하기 1"
author: JellyBrick
date: 2017-10-01 22:24
category: Report
tags: ["Programming", "Java", "Rhino", "JavaScript"]
---

자바로 만든 자바스크립트 엔진, Rhino에서 C로 짠 네이티브 라이브러리를 구동하는 방법을 소개하겠습니다.

## 준비물
JNA (Java Native Access)를 포함하여 컴파일된 Rhino 엔진

Java

(리눅스 기준)
gcc


## 방법

C코드 (HelloWorldLib.c)
```
char* helloWorld() {
    return "Hello World!"
}
```
이제 이 코드를 컴파일합니다. 
`gcc -fPIC -c HelloWorldLib.c`
`gcc -shared -o libHelloWorld.so HelloWorldLib.o`

컴파일이 완료되었으면 `libHelloWorld.so`가 생성되어 있을겁니다.
이제 이 라이브러리를 JNA를 이용하여 Rhino에서 호출해보겠습니다.

JavaScript코드
```
print(com.sun.jna.NativeLibrary.getInstance("경로/libHelloWorld").getFunction("helloWorld").invokeInt(new Array()));
```
`Hello World!`가 출력됩니다.

가독성이 심각하게 떨어지므로 코드를 분리해보겠습니다.

```
helloWorldLib = com.sun.jna.NativeLibrary.getInstance("경로/libHelloWorld");

result = helloWorldLib.getFunction("helloWorld").invokeInt(new Array());

print(result);
```

Hello World!가 출력됩니다.

이제 이 방법을 이용하여 C 텔레그램 라이브러리를 Rhino 엔진에서 사용하는 방법을 다음번에 소개하겠습니다.



