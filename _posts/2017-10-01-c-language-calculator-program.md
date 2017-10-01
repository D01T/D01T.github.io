---
title: "C언어 계산기"
author: 4season
date: 2017-10-01-11:45
category: Report
tags: ["Programming", "C", "Calculator"]
copyright: Delighit Lab
---
```+C
#include <stdio.h>

int main() { 
	int a, b; 
	char ch; 

	printf("첫번째 수를 입력하세요 : "); 
	scanf_s("%d", &a); 
	printf("연산자를 입력하세요(ex. +, -, *, /, %%) : "); 
	scanf_s(" %c", &ch, 1); 
	printf("두번째 수를 입력하세요 : "); 
	scanf_s("%d", &b); 

	if(ch =='+') { 
		printf("%d + %d = %d\n", a, b, a+b); 
	} 
	if(ch == '_') { 
		printf("%d - %d = %d 입니다. \n", a, b, a-b); 
	} 
	if(ch == '*') { 
		printf("%d * %d = %d 입니다. \n", a, b, a*b); 
	} 
	if(ch == '/') { 
		printf("%d / %d = %f 입니다. \n", a, b, (float)a/(float)b); 
	} 
	if(ch == '%') { 
		printf("%d %% %d = %d 입니다. \n", a, b, a%b); 
	} 
	return 0; 
} 
```
<br>

C언어로 만든 계산기 입니다. <br>
기능은 `더하기, 빼기, 곱하기, 니누기, 나눈나머지` 가 있습니다. <br>
(ps. 디버깅이 안되는 관계로 소스만 올리도록 하겠습니다..)
