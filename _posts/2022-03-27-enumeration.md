layout: single
title: "C++ 문법(8) : 열거형 (Enumeration)"
categories: Cpp
tag: [C++, Programming, Study]
toc: true
author_profile: true
search: true

# 열거형 (Enumeration)

**열거자 이름들은 일반적으로 해당 언어의 상수 역할을 하는 식별자**

## Const, Enum, #define

```C++
#include <iostream>
using namespace std;

// const란?
// C, C++에서 변수의 값이 바뀌는 것을 방지하기 위한 한정사
// 즉, 이 한정사가 붙은 변수는 상수로 취급

// 밑 코드는 const 셋트인데, 따로 노는 느낌이 듦
// const는 enum의 비해 약간의 메모리를 더 잡아먹을 수 있다
const int SCISSORS = 1;
const int ROCK = 2;
const int PAPER = 3;

// 해결 방법 !

// enum를 통해 상수를 하나의 셋트로 모을수 있음
// enum 값은 숫자를 지정하지 않아도 된다
// 숫자를 지정하지 않으면 첫 값은 0으로 시작
// 그 다음 값들은 이전 값 +1

enum ENUM_SRP
{
	ENUM_SCISSORS = 5 , // 5
	ENUM_ROCK, // 6
	ENUM_PAPER // 7
};

// const 에 비해 enum이 더 효율적

// #이 붙은거 -> 전처리 지시문!
// 1) 전처리(쉬운 작업) 2) 컴파일(통역) 3) 링크
// EX) #include <iostream> 이라는 파일을 찾아서 해당 내용을 복붙!
// #define은 상수 뿐만 아니라 코드 바꿔치기도 가능
// #define는 마지막 옵션으로 사용하기 (최대한 사용을 지양하기)

#define DEFINE_SCISSORS 1
#define DEFINE_TEST cout << "Hello World" << endl;
// 전처리단계가 끝나면 아예 사라짐
// 실행하면 존재하지 않음

int main()
{
	DEFINE_TEST;
}
```