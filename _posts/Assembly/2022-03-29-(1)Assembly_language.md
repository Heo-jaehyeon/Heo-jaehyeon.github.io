---
layout: single
title: "어셈블리어 문법(1) : 어셈블리어(Assembly language)에 대해"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
toc_sticky : true
author_profile: true
search: true
---



# 어셈블리어(Assembly language)

## 어셈블리어란?

**기호 언어**라고도 부르며 어셈블리어로 작성된 프로그램은 어셈블러에 의해 기계어로 번역되어야만 실행이 가능하다



사람으로써 이해하기 쉬운 언어로 작성한것을 기계어로 변환해주는 작업을

-> **컴파일러** 또는 **어셈블러** 라고 함 ( 그중에서도 NASM 어셈블러를 사용함 )

번역하는 과정을 통합어셈블러인 " **SASM** " 라는 프로그램이 도와주는 역할을 한다



# Hello World 출력하기

```c++
%include "io64.inc"

section .text
global CMAIN
CMAIN:
    ;write your code here
    
    PRINT_STRING msg
    
    xor rax, rax
    ret
    
section .data
    msg db 'Hello World', 0x00
```

코드 속에 **section .text** 와 **section .data**로 나누어져 있는것을 볼수있다

**주석 : 메모를 남길 수 있는 기능**

어셈블리에서는 **;** 로 주석을 달수 있다


# 실행파일 구조

![file_structure](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/file_structure.png?raw=true)

실행파일의 구조는 위의 사진처럼 보통 **코드(Section .text)**, **데이터(Section .data)**, **리소스(Section .rsrc) 섹션**에 나뉘어서 저장된다



# 컴퓨터 구조

![computer_structure](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/computer_structure.png?raw=true)

- **CPU**  : 중앙처리장치, 모든 연산을 담당

- **메인 메모리** : 컴파일이 완료된 프로그램 코드가 올라가서 실행되는 영역 

  ( 프로그램 실행을 위해 데이터를 일시적으로 저장하는 장치 )

  ex) 하드디스크 안의 게임을 실행하게 되면 메인 메모리로 올라가서 실행된다

  ( 실행파일 구조 부분에서 상단 부분의 **File** 과 **Memory** 구조의 차이를 살펴보자 )

