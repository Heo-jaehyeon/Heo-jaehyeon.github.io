---
layout: single
title: "어셈블리어 문법(6) : 분기문(Branch gate) 과 반복문(Iteration)"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
author_profile: true
search: true
---


# 분기문 (Branch gate)

**특정 조건에 따라서 코드 흐름을 제어하는 것**

ex) 스킬 버튼 눌렀는가? YES -> 스킬 사용

ex) 제한 시간 내에 던전 입장 수락 버튼을 눌렀는가?

YES -> 입장, NO -> 던전 취소

분기문은 **조건 -> 흐름**순으로 진행



**분기문(if) 방식**

**CMP <피연산자1>, <피연산자2> (피연산자1이 기준)**

cmp => compare의 약자



비교를 한 결과물은 **Flag Register**에 저장

​    

## JMP [label] 시리즈

c언어의 **goto 문**과 유사하다

**JMP** : 무조건 jump

**JE** : JumpEquals 같으면 jump

**JNE** : JumpNotEquals 다르면 jump

**JG** : JumpGreater 크면 jump

**JGE** : JumpGreaterEquals 크거나 같으면 jump



## 분기문 (Branch gate) 예시코드

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging

    ; 두 숫자가 같으면 1, 아니면 0을 출력하는 프로그램
    
    mov rax, 10
    mov rbx, 20
    
    cmp rax, rbx
    
    je LABEL_EQUAL
    
    ; je에 의해 점프를 안했다면, 같지 않다는 의미
    mov rcx, 0
    jmp LABEL_EQUAL_END
    
LABEL_EQUAL:
    mov rcx, 1
LABEL_EQUAL_END:

    PRINT_HEX 1, rcx
    NEWLINE
  
    ; 연습문제 : 어떤 숫자가 짝수면 1, 홀수면 0을 출력하는 프로그램
    
    mov ax, 91 ; 어떤 숫자가 91이라면
    
    ; 나누기 연산 - div bl => ax / bl (al 몫, ah 나머지)
    
    mov bl, 2
    div bl
    cmp ah,0 ; 나머지를 비교
    je L1
    mov rcx, 0
    jmp L2
L1:
    mov rcx, 1
L2:
    PRINT_HEX 1, rcx
    NEWLINE

    xor rax, rax
    ret
```



# 반복문 (Iteration)

c언어에서의 while, for, do-while과 같이

특정 조건을 만족할때까지 반복해서 실행하는 문



## Loop 문을 이용한 반복문

**loop [라벨]**

-**ecx에 반복횟수**를 저장

-loop 할때마다 ecx 1 감소, 0이면 빠져나감. 아니면 라벨로 이동



### 1에서 100까지의 합을 구하는 프로그램

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging
        
    mov ecx, 100
LABEL_LOOP_SUM:
    add ebx, ecx
    loop LABEL_LOOP_SUM
    
    PRINT_DEC 4, ebx
    NEWLINE
    
    xor rax, rax
    ret
```



## 분기문을 이용한 반복문

어셈블리어에서는 분기문 jump 시리즈문을 통해 반복문을 만들수 있다



### Hello World를 10번 출력하기

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging   
    mov ecx, 10 ; 10번을 실행하겠다라는걸 ecx에 저장
    
LABEL_LOOP:
    PRINT_STRING msg
    NEWLINE
    dec ecx ; sub ecx, 1과 동일 (dec는 decrease의 약자)
    cmp ecx, 0
    jne LABEL_LOOP

section .data
    msg db 'Hello World', 0x00
    
section .bss
    num resb 1
```



### 1에서 100까지의 합을 구하는 프로그램

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging

    mov eax, 100 ; 최종 목적지
    xor ebx, ebx ; mov ebx, 0 과 똑같은 의미, (ebx는 결과물을 저장)
    mov ecx, 0 ; ecx는 카운트
    
LABEL_SUM:
    inc ecx ; add ecx, 1 과 동일 (inc는 increas의 약자)
    add ebx, ecx ; ebx = ebx + ecx
    cmp ecx, eax ; 최종 목적지에 도달했는가?
    jne LABEL_SUM
    
    PRINT_DEC 4, ebx
    NEWLINE
```





