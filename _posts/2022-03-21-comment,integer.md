---
layout: single
title: "C++ 문법(1) : "주석(Comment)과 정수(Integer)""
categories: C++
tag: [C++, Programming, Study]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---


# 주석

##### 한 줄 주석 //

```c++
// 메모할 말 적기
```

##### 여러 줄 주석 /* */

```c
/*
메모할 말 적기
*/
```

##### 한번에 주석처리하는 간편한 단축키 

Ctrl+K+C (Comment), Ctrl+K+U(UnComment)



# 정수

##### 변수 선언 방법

```c++
#include <iostream>
using namespace std;

/*
변수 선언 방법 
[타입] [이름];
[타입] [이름] = [초기값];
*/

int hp = 100;
// 타입이 int인 hp라는 변수를 초기값 100으로 선언
// 0이 아닌 초기화 값이 있으면 .data 영역으로 그렇지 않으면 .bss 영역으로
 
char a; // 1바이트 = 8비트 (정수 -128 ~ 127)
short b; // 2바이트 = 16비트 (-32768 ~ 32767)
int c; // 4바이트 (-21.4억 ~ 21.4억)
__int64 d; // 8바이트(long long) (엄청 큼)
// int, char, short, __int64 앞에 signed 가 생략되어있다.
// signed 는 양수와 음수를 모두 포함
// char == signed char는 같은 의미

unsigned char f; // unsigned 타입은 양수만 취급 (0 ~ 255)
unsigned short g; // (0 ~ 65536)
unsigned int h; //  (0 ~ 42.9억)
unsigned __int64 j; // (엄청 큼)

int main()
{
    cout << "체력이 " << hp << " 남았습니다" << endl;
// "체력이 100 남았습니다" 를 출력
}
```

##### 오버플로우와 언더플로우

```c++
b = 32767;
b = b+1;
cout << b << endl; // -32768 -> 정수 오버플로우
g = 0;
g = g - 1;
cout << g << endl; // 65535 -> 정수 언더플로우
```



Q : 대충 4바이트인 타입 int로만 선언하면 안될까?

A : 콘솔/모바일 게임 개발 같은 경우에는 메모리가 늘 부족  !

​	 온라인 게임의 경우 동접자가 많기 때문에 메모리 관리가 필수적 !
