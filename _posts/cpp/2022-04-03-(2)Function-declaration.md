---
layout: single
title: "C++ 문법(11) : 함수 선언(Function declaration)"
categories: Cpp
tag: [C++, Programming, Study]
toc: true
toc_sticky : true
author_profile: true
search: true
---


# 함수 선언 (Function declaration)

```c++
#include <iostream>
using namespace std;

void Func1()
{
	cout << "Func1" << endl;
	Func2(1,2); 
}

void Func2(int a, int b)
{
	cout << "Func2" << endl;
	
}

int main()
{
	cout << "main" << endl;
	Func1();
	return 0;
}
```

위 코드를 실행하면  **Func2 함수가 정의되지 않았다는 컴파일 오류**가 발생하게 된다

그 이유는 **C 컴파일러는 위에서 아래로 소스 코드를 해석하는데 Func1 함수 속에서는**

**아직 Func2 함수에 대한 정보가 없었기 때문이다**



따라서 이러한 문제를 해결 하기 위해서는

어떠한 함수가 존재한다는 사실을 먼저 주어야하는데 이를 **함수 선언**이라고 한다

함수 선언은 함수의 원형만 선언해주면 되는데

```c++
#include <iostream>
using namespace std;

// 함수 선언
void Func1();
void Func2(int a, int b);

void Func1()
{
	cout << "Func1" << endl;
	Func2(1,2); 
}

void Func2(int a, int b)
{
	cout << "Func2" << endl;
}

int main()
{
	cout << "main" << endl;
	Func1();
	return 0;
}
```

void Func1(); 과 같이 반환값 자료형, 함수의 이름, (), 세미콜론을 붙여주면 

Func1 이라는 함수가 밑에 존재한다는 사실을 알려줄 수 있다



참고)

void Func2(int a, int b); 같은 경우는 void Func2(int, int); 처럼

**매개변수의 이름을 생략해줄수 있다**
