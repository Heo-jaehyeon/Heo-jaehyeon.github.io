---
layout: single
title: "어셈블리어 문법(4) : 변수(Variable)와 레지스터(Register)"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
author_profile: true
search: true
---

# section. text

메모리 <-> 레지스터를 자유자재로 넘나들수 있다

**text 영역은 실제 코드를 유지하는데 사용된다**



# section. data

**data 영역에서는 초기화 된 데이터를 선언할 수 있다**

**[변수이름] [크기] [초기값]** 의 형식으로 선언할수 있다

**[크기] 값에는 db(1), dw(2), dd(4), dq(8)**이 들어간다

ex )

```c++
section .data
	a db 0x11
	b dw 0x2222
```



# section .bss

**bss 영역에서는 초기화 되지 않은 데이터를 선언할 수 있다**

**[변수이름] [크기] [개수]** 의 형식으로 선언할수 있다

**[크기] 값에는 resb(1byte),  resw(2byte), resd(4byte), resq(8byte)**이 들어간다

ex )

```c++
section .bss
	e resb 10
```



# .data 와 .bss가 나누어진 이유

data 영역은 초기화 할때 전부 실행파일인 exe 파일안에 저장되어 있다

반면 초기화 되지 않은 데이터들은 초기에 0으로 셋팅만 하면 되므로 실행 파일에 따로 저장할 필요가 없다

**즉 어차피 최종적인 크기만 알고 있으면 파일값에다 어떤 값으로 초기화 해야되는지 지정할 필요가 없으므로 파일의 크기를 줄이는 효과가 있다**



# .data 와 .bss 의 예시코드

```c++
%include "io64.inc"

section .text

    ; 변수의 선언 및 사용
    ; 변수는 그냥 데이터를 저장하는 바구니 [ ]
    ; 처음에 바구니 사용하겠다 선언 (이름과 크기 지정)
    
    ; 메모리에는 구분할수 있도록 주소(번지수)가 있다
    
global CMAIN
CMAIN:
        mov rbp, rsp; for correct debugging
    
    mov rax, a ; a라는 바구니 주소값을 rax에 복사 (메모리에 있는걸 레지스터에 긁어오는 작업)
    mov rax, [a] ; a라는 바구니 안에 있는 값을 rax에다 복사
                 ; 그러나 바구니 범위를 넘어서 옆에있는 값까지 가져옴
                 ; mov 명령어는 양쪽 다 크기가 같아야함
    
    mov al, [a] ; 
    
    mov [a], byte cl ; (레지스터에서 메모리로 긁어오는 작업)
    mov [a], word 0x6666
        
    xor rax, rax
    ret
    
    
section .data
 
    a db 0x11   ; [0x11]
    b dw 0x2222
    c dd 0x33333333
    d dq 0x4444444444444444
    
section .bss

    e resb 10
    
```



**참고사항 )**

![memory](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/memory.PNG?raw=true)

1) mov rax, a 명령어는 rax에 0x403010를 넣는다 따라서 주소값이 아닌 mov rax, [a] 명령어와 같이 a라는 주소에 바구니를 씌워서 변수에 저장된 값을 보내줘야 한다

2) a 변수와 b 변수의 value 값을 보면 b가 a의 메모리 바로 옆에 값이 저장되어 표시되는것을 볼수 있다
