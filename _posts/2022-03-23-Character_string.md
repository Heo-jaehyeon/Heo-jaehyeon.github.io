---
layout: single
title: "C++ 문법(3) : 문자(Characters)와 문자열(Strings)"
categories: C++
tag: [C++, Programming, Study]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true
---

# 문자(Characters)

문자(char)는 정수지만 '문자' 의미를 나타내기 위해 사용 (bool과 같음)

```c++
#include <iostream>
using namespace std;

// 문자(char)는 정수지만 '문자' 의미를 나타내기 위해 사용 (bool과 같음)
// char 타입 : 알파벳 / 숫자 문자를 나타냄
// wchar_t : 유니코드 문자를 나타냄 (UTF16)

char ch = 97;
char ch1 = 'a'; // ch와 같음
char ch2 = '1';
char ch3 = 'a' + 1;


wchar_t wch = L'안';
// L은 유니코드를 인식

int main()
{
	cout << ch << endl;
	// 문자 a가 출력
	cout << ch2 << endl;
	// 문자 1이 출력
	cout << ch3 << endl;
	// 문자 b가 출력
	cout << wch << endl;
	// 50504 출력
	// why? cout은 char 전용
	wcout << wch << endl;
	// 문자 '안' 출력
}
```



## 아스키코드(ASCII)

ASCII (American Standard Code for Information Interchange)

문자의 의미로 작은 따옴표 '' 사용

![ASCII_Table](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/ASCII_Table.jpg?raw=true)

## 유니코드(Unicode) 

**전 세계 모든 문자에 대해 유일 코드를 부여한 것**

**영어만 표현한 ASCII 한계를 극복한 코드** 

유니코드는 표기 방식이 여러가지가 있음(UTF8, UTF16)

### UTF8 (서양권에서 사용)

- 알파벳, 숫자 1바이트 (ASCII 동일한 번호)

- 유럽 지역의 문자는 2바이트

- 한글, 한자 등 3바이트

### UTF16 (동아시아권에서 사용)

- 알파벳, 숫자, 한글, 한자 등 거의 대부분 문자 2바이트

- 고대문자만 4바이트

## Escape Sequence

**표기하기 애매한 애들을 표현**
   
\0 = 아스키코드0 = NULL   
\t = 아스키코드9 = Tab   
\n = 아스키코드10 = LineFeed (한줄 아래로)   
\\'

# 문자열(Strings)

**문자들이 열을 지어서 모여 있는 것**   

**맨 끝에는 \0 이 저장되어있다 (NULL(0))**

```c++
#include <iostream>
using namespace std;

// 문자열 선언하는 방법

char str[] = {'h','e','l','l','o','\0'};
char str2[] = "Hello World"; // 12글자(NULL 포함)

int main()
{
	cout << str << endl;
	// hello 출력
	cout << str2 << endl;
	// Hello Wolrd 출력
}
```
