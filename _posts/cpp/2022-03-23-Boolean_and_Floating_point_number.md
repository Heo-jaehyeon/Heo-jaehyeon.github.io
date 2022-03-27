---
layout: single
title: "C++ 문법(2) : 불리언 (Boolean)과 부동소수점 (Floating point number)"
categories: Cpp
tag: [C++, Programming, Study]
toc: true
author_profile: 
search: true
---

# 불리언 (Boolean)

```c++
#include <iostream>
using namespace std;

// 불리언(boolean) = 참/거짓(1바이트)
bool isHighLevel = true;
bool isPlayer = true;

int main()
{
	cout << isHighLevel << endl;
	// 1이 출력된다
	// False는 0. True는 1를 나타냄
}
```

# 부동소수점 (Floating point number)

실수 (부동소수점) -> ex) 3.14

부동소수점은 .을 유동적으로 움직여서 표현하는 방법

## 부동소수점에 대한 이해

### 정규화 과정

3.141592 = 0.3141592 * 10^1 

유효숫자는 3145192 지수는 1



ex) -3.375 정규화 하는법

2진수 변환 = (3) + (0.375) = 0b11 + 0b0.011 = 0b11.011
0.375 = 0.5 * 0 + 0.25 * 1 + 0.125 * 1 = 0b0.011

정규화 0b1.1011 * 2^1

부호(1), 지수(1), 유효숫자(1011)

단 지수는 unsigned byte라고 가정하고 숫자+127를 만들어줌

예상 결과 : 0b 1 10000000 1011000 0000 0000 0000 0000

```c++
// 타입 float(4바이트=32비트), double(8바이트=64비트)
// float 부호(1비트), 지수(8비트), 유효숫자(23) = 32비트 = 4바이트
// double 부호(1), 지수(11), 유효숫자(52) = 8바이트

float attackSpeed = 0.639f;
// 실수를 float 타입으로 사용하고 싶을때는 f를 붙여줘야함
// f 안붙이면 기본적으로 double 타입으로 설정
double attackSpeed2 = 123.4123;
```

**프로그래밍할 때 부동소수점은 항상 '근사값'이라는 것을 기억해야한다!**

**수가 커질수록 오차 범위도 매우 커짐!**

**실수 2개를 == 으로 비교하는 것은 지양하기!**
