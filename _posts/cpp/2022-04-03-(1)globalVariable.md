---
layout: single
title: "C++ 문법(10) : 지역변수(Localvalue)와 전역변수(Globalvalue), 함수의 값 전달"
categories: Cpp
tag: [C++, Programming, Study]
toc: true
author_profile: true
search: true
---

# 전역 변수 (Globalvalue)

값이 유지되기 때문에 어디에서든 접근 가능하다

Main 함수 실행가 실행되기 전, 프로그램이 실행되자 마자 메모리에 할당됨.

프로그램이 끝나는 순간 메모리에서 해제된다

**전역 변수는 Stack 영역이 아닌 Data 영역에 들어간다**



# 지역 변수 (Localvalue)

매번 새로운 값 생성되고 값의 유지가 안된다

함수가 실행되는 순간마다 메모리에 할당되고 함수가 종료되는 순간에는 메모리에서 해제됨

**지역 변수는 Stack 영역에 저장된다**

**큰 규모의 프로그램이라면 전역 변수보다는 지역 변수를 최대한 활용해야한다**



# 예시코드

```c++
#include <iostream>
using namespace std;

// 전역 변수
int globalValue = 0;

void Test()
{
	cout << "전역 변수의 값은 : " << globalValue << endl;
    // 전역변수 globalValue는 어디서든지 접근이 가능함
}

void IncreaseHp(int hp)
{
	hp = hp + 1;
}

// STACK 구성
// [매개변수][RET주소][지역변수(hp=1)] [매개변수(hp=1->hp=2)][RET주소][지역변수] 

int main()
{
	Test(); // 전역 변수의 값은 : 0 출력
	
	int localValue = 1; // 지역 변수
	
	int hp = 1;
	
	cout << "Increase 호출 전 : " << hp << endl; // 결과 1
	IncreaseHp(hp);
	cout << "Increase 호출 후 : " << hp << endl; // 결과 1

  // 위 3줄 코드 에서,
  // hp가 왜 증가하지 않고 1 일까?
	// main 함수의 지역변수 hp를 건들인것이 아닌
	// 매개변수에 들어간 hp를 조작했기 때문이다
	
	// 매개변수 hp가 아닌 지역변수 hp를 건들이기 위해서는?
	// 포인터를 사용하면 된다!
	
	return 0;
}
```

