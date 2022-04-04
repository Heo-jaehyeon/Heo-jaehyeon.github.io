layout: single
title: "C++ 문법(12) : 함수 마무리"
categories: Cpp
tag: [C++, Programming, Study]
toc: true
author_profile: true
search: true



# 오버로딩 (Overloading)

**오버로딩 = ( 중복정의 : 함수이름을 재사용하는것 )**

매개변수의 갯수가 다르거나 매개변수 타입이 다르다면 ( 순서가 다른걸 포함 )

**함수 이름을 재사용** 할수 있다

```c++
#include <iostream>
using namespace std;

// 오버로딩

int Add(int a, int b)
{
	int result = a + b;
	return result;
}

float Add(float a, float b)
{
	float result = a + b;
	return result;
}

int main()
{
	float result = Add(1.5f, 2.1f); // float Add 함수 사용
	cout << result << endl;
    
    int sum = Add(1,2); // int Add 함수 사용
    cout << sum << endl;

	return 0;
}
```

**참고) 반환 타입만 다르면 컴파일이 되지 않는다**



# 함수 기본 인자값

기본 인자값은 꼭 **매개 변수 맨 끝**에 넣어야 한다

```c++
#include <iostream>
using namespace std;

// 기본 인자값

void SetPlayerInfo(int hp, int mp, int attack, int guildid = 0, int castleId = 0)
{
}

int main()
{
	SetPlayerInfo(100, 40, 10);
    // SetPlayerInfo 함수 선언시 매개변수에 기본 인자값을 맨끝에 넣어주면
    // 함수를 호출할때 매개변수를 넣어주지 않아도 기본 인자값으로 처리된다
    
	SetPlayerInfo(100, 40, 10, 0, 1);
    // 매개변수를 다르게 하고싶을때는 다시 넣어줘도 된다
	
	return 0;
}
```



# 스택 오버플로우 (Stack overflow)

함수의 재귀호출이 무한히 반복되면, 해당 프로그램은 스택 오버플로우에 의해 종료된다

함수를 계속 호출해 스택의 모든 공간을 다 차지한 후 또 다시 스택 프레임을 넣게 되면

해당 데이터는 스택 영역을 넘어가서 저장한다

![stackoverflow](C:\Users\307대대\Desktop\stackoverflow.png)

이는 **보안상의 큰 취약점**이나 **오동작**을 일으키게 하므로

C 언어에서는 스택 오버플로우가 **발생**하면 **에러를 발생**시킨다



```c++
#include <iostream>
using namespace std;

// 스택 오버플로우

int Factorial(int n)
{
	// 5! = 5*    4!
	// 4! = 4*    3!
	// n! = n*   (n-1)!
	
	if (n <= 1)
		return 1;
	
	return n * Factorial(n-1);
}

int main()
{
	int result2 = Factorial(5); // 120 출력 
	cout << result2 << endl;
	
	int result3 = Factorial(100000); // 스택 오버플로우 발생
	cout << result3 << endl;
	
	return 0;
}
```

