---
layout: single
title: "어셈블리어 문법(5) : 문자(Character), 엔디안(Endian), 연산(Calculation)"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
author_profile: true
search: true
---

# 문자 (Character)

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging
    
    PRINT_STRING msg ; msg 변수 출력
    
    xor rax, rax
    ret
    
section .data
    msg db 'Hello World', 0x00 
    ; msg db 0x48,0x65,0x6c,0x6c,0x6f,0x20,0x57,0x6f,0x72,0x6c,0x64,0x0 
    ; 와 같은 의미
    
    a db 0x11, 0x11, 0x11, 0x11
    ; 바구니를 만들때 쉼표로 구분해서 일련의 데이터를 저장할수 있다
    
    b dd 0x12345678
    ; 메모리에 0x12345678 를 대입  
```

![msg](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/msg.PNG?raw=true)

msg 라는 변수에 db(1byte) 크기로 Hello World 문자열을 저장할때,

msg value 값에는 각 영어문자를 표현하는 **아스키 코드**가 들어가고

맨끝에는 C++와 같이 문자열의 끝을 알리는 **0x00**이 저장 되어있다



## 빅 엔디언 (Big Endian)

**보통 큰 단위가 앞에 나오는 방식**

위에 나와있는 코드처럼, b라는 변수 메모리에 0x12345678 를 대입했을때

value 값이 0x12, 0x34, 0x56, 0x78 순으로 나온다면 이는 빅 엔디언 방식이다

( 사람이 숫자를 쓰는 방법과 같다 )

**장점 : 숫자 비교에 유리하다, 소프트웨어의 디버그를 편하게 해준다**

<- 높은 주소 - - - - 낮은 주소 ->



## 리틀 엔디언 (Little Endian)

보통 작은 단위가 앞에 나오는 방식

위에 나와있는 코드처럼, b라는 변수 메모리에 0x12345678 를 대입했을때

value 값이 0x78, 0x56, 0x34, 0x12 우리가 알던 방식과 다르게,

데이터의 단위로 나누었을때의 역순으로 나온다면 이는 **리틀 엔디언 방식**이다

**장점 : 캐스팅에 유리하다**  

<- 낮은 주소 - - - - 높은 주소 ->



# 연산 (Calculation)

### **덧셈 연산 방식**

**add** a, b  즉 (a = a + b)



a는 **레지스터 or 메모리**

b는 **레지스터 or 메모리 or 상수**

**단 a, b 모두 메모리면 안된다**



### 뺄셈 연산 방식

**sub** a, b 즉 (a = a - b)



**뺄셈 방식과 규칙은 더하기 연산과 같다**



### 곱하기 연산 방식

**mul 레지스터**



mul bl 의 의미 : **al * bl**

 -- 연산 결과를 **ax**에 저장

mul bx => **ax * bx**

 -- 연산 결과는 **dx(상위16비트) ax(하위16비트)**에 저장

mul ebx => **eax * ebx**



### 나누기 연산 방식

**div 레지스터**



div bl 의 의미 :  **ax / bl**

-- **연산 결과는 al (몫), ah (나머지)에 저장된다**



### 사칙연산 예시코드

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    mov rbp, rsp; for correct debugging
    
    GET_DEC 1, al
    GET_DEC 1, num
    
    add al, 1 ; a : 레지스터 b : 상수
    PRINT_DEC 1, al ; 1+1=2
    NEWLINE
    
    add al, [num] ; num은 값이 들어가 있는것이 아니라 주소가 들어있음 따라서 [num]으로 바구니를 씌어줘야한
    PRINT_DEC 1, al ; 2+2=4
    NEWLINE
    
    mov bl, 3
    add al, bl ; 레지스터 + 레지스터
    PRINT_DEC 1, al ; 4+3=7
    NEWLINE
    
    add [num], byte 1 ; 메모리 + 상수
    PRINT_DEC 1, [num] ; 2+1=3
    NEWLINE
    
    add [num], al ; 메모리 + 레지스터  
    PRINT_DEC 1, [num] ; 3+7=10
    NEWLINE
    
    ; 빼기 연산
    ; 빼기 규칙은 더하기 연산과 같다
    
    ; 곱하기 연산
    ; ex) 5 * 8 은?
        
    mov ax, 0
    mov al, 5
    mov bl, 8
    mul bl
    PRINT_DEC 2, ax ; 결과값 40
    NEWLINE
    
    ; 나누기 연산  
    ; ex) 100 / 3 은?

    mov ax, 100
    mov bl, 3
    div bl
    PRINT_DEC 2, al ; 몫 33 출력
    NEWLINE
    mov al, ah ; ah는 PRINT_DEC 로 출력할수 없음
    PRINT_DEC 1, al ; 나머지 1 출력
    
    xor rax, rax
    ret
    
section .bss
    num resb 1
```

