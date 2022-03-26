---
layout: single
title: "C++ 문법(7) : 반복문 (Iteration)"
categories: C++
tag: [C++, Programming, Study]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

# 반복문 (Iteration)

## While 반복문

while ~동안에

**한번만 실행하는게 아니라, 특정 조건까지 계속 반복해야하는 상황일때 사용**

```c++
#include <iostream>
using namespace std;


int main()
{

	/*
	
	while 반복문 구조
	
	while (조건식)
	{
		명령문
	}
	*/
	
	int count = 0;
	
	while (count < 5)
	{
		cout << "Hello World" << endl;
		count++;
	}
```



### do while 반복문

while 반복문과의 차이점

**do 괄호안에 있는 명령문은 한번은 무조건 실행**

```c++
/*
	do while 반복문 구조
	
	do
	{
		명령문
	} while (조건식)
	
*/
	
	do
	{
		cout << "Hello World" << endl;
	} while (false);
	// Hello Wolrd 한번 출력
	// 거의 사용하지 않는 반복문임
```



## for 반복문

**반복횟수가 정해져 있을때 주로 사용**

사용빈도수 (for 반복문) 9:1 (while 반복문)

```c++
/*
	
	for 반복문 구조
	
	for (초기식; 조건식; 제어식)
	{
		명령문
	}
	
	*/
	
	for (int i = 0; i < 5; i++)
	{
		cout << "Hello World" << endl;
	}
	// Hello World 5번 출력
*/
```



# 반복문의 흐름 제어

## Break

**Break 사용 구조**

```c++
while (조건식)
	{
		명령문
		
		break;
		// break의 의미 : 반복문에서 빠져나가주세요
	}
```



**While 중첩 사용 시 Break 활용**

```c++
	
while (조건식1)
{
	while (조건식2)
	{
		명령문
		
		break;
		// 괄호 하나만 빠져나감
	}
}

```



### Break를 활용한 게임 전투 방식

```c++
#inlcude <iostream>
using namespace std;

int round = 1;
int hp = 100;
int damage = 10;

// 무한루프 : 전투시작
while (true)
{
	hp -= damage;
	if (hp < 0)
		hp = 0; // 음수 체력을 0으로 보정
	
	// 시스템 메시지
	count << "Round " << round << " 몬스터 체력" << hp << endl;
	
	if (hp == 0)
	{
		cout << "몬스터 처치!" << endl;
		break;
		// if문을 나가는것이 아니라 while문을 나감
	}
	
	if (round == 5)
	{
		cout << "제한 라운드 종료" << endl;
		break;
	}
}

round++;
```



## Continue

**continue 사용 구조**

```c++
while (조건식)
{
	continue;
	// 반복문을 한번 빠져나간뒤 다시 반복 실행
	명령문
} 
```



### Continue를 활용한 정수 1~10 사이의 홀수 출력

```c++
#include <iostream>
using namespace std;

for (int k = 1; k <= 10; k++)
{
	bool isEven = ((count % 2) == 0);
	
	if (isEven)
		continue;
	
	cout << k << endl;
}
```
