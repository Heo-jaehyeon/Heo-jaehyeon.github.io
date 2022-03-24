---
layout: single
title: "C++ 문법(4) : 데이터 연산(Data operation)"
categories: C++
tag: [C++, Programming, Study]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---


# 데이터 연산 (Data operation)

## 사칙 연산 (the four fundamental arithmetic operations)

```c++
#include <iostream>
using namespace std;

// 사칙 연산

int a = 1;
// a라는 이름의 바구니를 할당하고 안에 1를 넣는다
int b = 2;

int main()
{

	a = b; // 대입연산
	
	a = b + 3; // 덧셈 add
	a = b - 3; // 뺄셈 sub
	a = b * 3; // 곱셈 mul
	a = b / 3; // 나눗셈 div
	a = b % 3; // 나머지 div
	
	a += 3; // a = a + 3;
	a -= 3; // a = a - 3;
	a *= 3; // a = a * 3;
	a /= 3; // a = a / 3;
	a %= 3; // a = a % 3;
	
	// 증감 연산자
	a++;
	++a;
	a--;
	--a;
	
	// ex)
	b = a++; // a를 b에 대입 후 a를 1 증가
	b = ++a; // a를 1증가 한 후 a를 b에 대입
	
	b = a + 1 * 3; // 곱셈,나눗셈 한 후 덧셈,뺄셈 실행
	
}
```



## 비교 연산 (Comparison operation)

```c++
#include <iostream>
using namespace std;

// 비교 연산

bool isSame;
bool isDifferent;
bool isGreater;
bool isSmaller;

int main()
{
	// a == b : a와 b의 값이 같은가?
	// 같으면 1, 다르면 0
	isSame = (a == b);
	
	// a != b : a와 b의 값이 다른가?
	isDifferent = (a != b);
	
	// a > b : a가 b보다 큰가?
	// a >= b : a가 b보다 같거나 큰가?
	isGreater = (a > b);
	
	// a < b : a가 b보다 작은가?
	// a <= b : a가 b보다 작거나 같은가?
	isSmaller = (a < b);
	
}
```



## 논리 연산 (Logical operation)

```c++
#include <iostream>
using namespace std;

// 논리 연산

bool isSame;
bool test;

int a = 1;
int b = 1;

int hp = 100;
bool isInvincible = true;

isSame = (a == b);

int main()
{
	test = !isSame;
	// ! 의 뜻 not
	// 0이면 1, 그 외 0
	// test 값 0
	
	test = (hp <= 0 && isInvincible == false); // 죽음!
	// && 의 뜻 AND
	// a && b -> 둘 다 1이면 1, 다르면 0
	
	test = (hp > 0 || isInvincible == true); // 살았음!
	// || 의 뜻 OR
	// a || b -> 둘 중 하나라도 1이면 1 (둘 다 0이면 0)
}
```



## 비트 연산 (Bit operation)

```c++
#include <iostream>
using namespace std;

// 비트 연산

// 언제 필요한가?
// 비트 단위의 조작이 필요할 때
// 대표적으로 비트플래그(Bitflag)

// - bitwise not
// 단일 숫자의 모든 비트를 대상으로, 0은 1, 1은 0으로 뒤바꿈

// & bitwise nand
// 두 숫자의 모든 비트 쌍을 대상으로, and를 한다

// | bitwise or
// 두 숫자의 모든 비트 쌍을 대상으로, or를 한다

// ^ bitwise xor
// 두 숫자의 모든 비트 쌍을 대상으로, xor를 한다
// xor 란? 두 숫자가 같으면 0, 다르면 1로 출력

// 비트시프트(bitshift)

// << 비트 좌측 이동
// 비트열을 N만큼 왼쪽으로 이동
// 왼쪽에 넘치는 N개의 비트는 버림, 새로 생성되는 N개의 비트는 0
//	*2를 할 때 자주 보이는 패턴

// >> 비트 우측 이동
// 비트열을 N만큼 오른쪽으로 이동
// 오른쪽의 넘치는 N개의 비트는 버림
// 왼쪽 생성되는 N개의 비트는
// - 부호 비트가 존재할 경우 부호 비트를 따라감 (부호있는 정수라면 이 부분을 유의)
// - 아니면 0 (unsigned 타입이면 무조건)

// 실습
// 0b0000 [무적][변이][스턴][공중부양]

unsigned char flag; // 부호를 없애야 >> 를 하더라도 부호비트가 딸려오지 않음

int main()
{
	flag = (1 << 3);
	// 1이라는 숫자를 왼쪽으로 3칸 이동
	// flag = 8 와 같은 명령어 (숫자가 너무 커지면 오히려 불편)
	// 무적 상태로 만든다
	
	flag |= (1 << 2);
	// 변이 상태(무적 + 변이)
	// flag |= 4; 와 같은 명령어
	
	// 무적인지 확인하고 싶다면? (다른 상태는 관심 없음)
	// Bitmask
	bool invincible = ((flag & (1 << 3)) != 0);
	
	// 무적이거나 스턴 상태인지 확인하고 싶다면?
	bool stunOrInvincible = ((flag & 0b1010) != 0);
	// 이렇게 하거나 또는
	bool mask = (1<<3) | (1 << 1);
	bool stunOrInvincible = ((flag & mask) != 0);
	// 이런식으로도 가능 !
}
```

