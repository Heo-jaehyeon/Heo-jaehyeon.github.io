---
layout: single
title: "어셈블리어 문법(8) : 스택 프레임 (Stack frame)"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
author_profile: true
search: true
---


# 스택 프레임 (Stack frame)

exe 파일 속 메모리 구조를 살펴보면

**코드(text)** 부분은 프로그램의 명령어가 저장되는 영역이고

**데이터(Data)** 부분은 초기화된 전역변수, 상수가 할당되는 영역이다

**BSS** 부분은 초기화하지 않은 전역, 정적 변수가 할당되는 영역이다



만약 코드가 실행될때 즉, 실행되는 도중의 프로그램의 메모리 구조는 아래와 같다



![process](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/process.png?raw=true)



메모리 구조에서 **힙(Heap)** 과 **스택(Stack**)이 추가된것을 볼수 있다

**힙(Heap)**은 동적으로 할당되는 데이터들이 쌓이는 영역이고

**스택(Stack**)은 코드에 있는 함수들이 호출될때마다 선언되고 사용되는 지역변수가 쌓이는 공간이다

참고로 **스택은 높은 주소에서 낮은 주소를 향해 데이터가 쌓인다**



대부분의 프로그램은 함수로 구성되어있다

함수 호출에 의한 스택프레임의 결과는 아래와 같다



![stackframe(1)](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/stackframe(1).png?raw=true)



프로그램이 실행되면 main 함수가 호출되면서 관련된 스택 프레임이 스택에 저장된다

뒤이어 func1() 함수를 호출하면 그 위에 func1() 함수의 **매개변수, 변환 주소값, 지역변수** 등의

스택 프레임이 스택에 저장되는 것을 볼수있다

func2()도 func1() 의 함수 스택 저장 과정과 동일하게 이루어진다





![stackframe(2)](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/stackframe(2).png?raw=true)

func2() 함수 작업이 끝나서 반환되면 스택 속에서 func2()의 스택프레임이 제거 되고

func1, main() 함수도 뒤이어 작업이 끝나면 스택에서 각 스택프레임이 제거된 후 프로그램이 종료된다 



**ex) 웹브라우저의 뒤로가기 기능은 스택구조의 예시로 들수있다**



# 명령어 [Push, Pop, Call]

레지스터는 다양한 용도로 사용



**포인터 레지스터** (포인터 = 위치를 가리키는 ~)

-- **ip (Instruction Pointer**) : 다음 수행 명령어의 위치

-- **sp (Stack Pointer)** : 현재 스택 top 위치 (일종의 cursor)

-- **bp (Base Pointer)** : 스택 상대주소 계산용



Stack Pointer 레지스터에는 현재 스택 top 위치가 저장되어 있는데 **push**와 **pop** 명령어로 조작할수 있다



## Push

(사용법) 

**push 값**



**push는 상태값을 스택에 차례대로 넣을수 있다 **



## Pop

(사용법)

**pop 레지스터**



**pop은 레지스터에서 값을 꺼내올수 있다**



## **Call (call a Procedure)**

함수 호출시 사용되며, JMP 명령어와 같이 프로그램 실행 흐름이 변경되지만 되돌아올 return 주소를 스택에 저장한다 

되돌아 올 주소를 저장하기 때문에 함수 호출 후 원래 위치로 실행흐름을 되돌릴 수 있으며

호출한 함수가 일을 다 마치면 원래 위치에서 다시 프로그램이 실행될 수 있다



# 예제코드

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging
    
    push 1 
    push 2
    call MX:
    PRINT_DEC 8, rax
    NEWLINE
    add rsp, 16
    
    xor rax, rax
    ret
    
MX:
    push rbp
    mov rbp, rsp
    
    mov rax, [rbp+16]
    mov rbx, [rbp+24]
    cmp rax, rbx
    jg L3
    mov rax, rbx
    
L3:
    pop rbp
    ret
    
    pop rbp
    ret
    
    
section .data
    msg db 'Hello World', 0x00
```

