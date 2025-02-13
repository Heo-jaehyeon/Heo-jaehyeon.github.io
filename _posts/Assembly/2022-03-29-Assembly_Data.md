---
layout: single
title: "어셈블리어 문법(2) : 데이터(Data) 기초"
categories: Assembly
tag: [Assembly, Programming, Study]
toc: true
toc_sticky : true
author_profile: true
search: true
---

# 데이터(Data) 기초

## 비트(Bit) 와 바이트(Byte)

![bit_bite](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/bit_bite.jpeg?raw=true)

### **비트란** **?** 

컴퓨터에서 사용하는 가장 작은 정보 단위 ( 이진수로 구성된 숫자 체계 )

**1 바이트 (Byte) = 8 비트 (Bit)**



## 2진수 데이터의 표현

![bit2](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/bit2.png?raw=true)



### 2진수를 10진수로 변환하는 방법


1001 (2진수) =1×2^3+0×2^2+0×2^1+1×2^0 = 9 (10진수)


2진수에서 **가장 오른쪽 비트를 최하위 비트**라 하고, **가장 왼쪽 비트를 최상위 비트**라고 한다

**가중치는 2**를 가지고 있다

예를 들어

![1byte](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/1byte.PNG?raw=true)



위 표와 같이 최하위 비트부터 최상위 비트까지 각 자리수가 2라는 가중치를 두고 있으며

0000 1101 이라는 2진수는 밑에 있는 수식처럼 가중치 (2) 를 비트가 1인 숫자에 곱해줘서 10진수로 표현 할 수 있다


00001101(2진수)= 1×2^0+0×2^1+1×2^2+1×2^3+0×2^4+0×2^5+0×2^6+0×2^7=13(10진수)



## 컴퓨터에서 양수와 음수를 표현하는 방법

**바이트 크기에 따라서 최상위 비트가 정수의 부호를 표시함**

![bit](https://github.com/Heo-jaehyeon/Heo-jaehyeon.github.io/blob/master/images/bit.png?raw=true)



최상위 비트가 **0이면 양수**를 의미하고, **1이면 음수를** 의미한다



## 2의 보수

1의 보수 ( 각 자리의 비트가 0이면 1로, 1이면 0으로 변경) 결과에 1를 더하여 

양수에서 음수 또는 그 반대로 바꿔줄 수있다 



ex) 

0101 0110 (2진수) = 86 (10진수)로 나타낼수 있는데 양수를 음수로 바꾸려면

1의 보수 처리 -> 1010 1001 (2진수)로 바꾼 후 1 (10진수) 를 더해준다

1010 1010 (2진수) = -86 (10진수)로 간편하게 2의 보수를 통해 바꿀수 있다



## 10진수, 2진수, 16진수

### 10진수란?

0, 1, 2, 3, 4, 5, 6, 7, 8, 9 까지의 10개의 숫자를 사용하고, 9 다음의 수로 자리올림을 발생하여

수를 표시하는 표기법 

ex) 10 11 12 13 ... 19 20

​    

### 2진수란?

0, 1 두 종류의 숫자로 수를 표시하는 표기법

**비트(Bit)와 같은 의미**를 가지고 있다

0 1 10 11 011 100 101 110 111 ...

2진수는  **0b를 앞에 붙여서 표시**함

0b10 = 2 ( 10진수 )

0b11 = 3 ( 10진수 )



### 16진수란?

0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F  까지의 16개의 숫자와 문자를 사용해 수를 표시하는 표기법

0 1 2 3 4 5 6 7 8 9 A B C D E F 10...

**16진수는 0x를 앞에 붙여서 표시**함 

0xA = 10 ( 10진수 )

0xB = 11 ( 10진수 )



**16진수에서 2진수로 왔다갔다 전환하는것은 매우 편함**

0b 1001 0101 = 0x95 (4개씩 끊어서 읽으면 16진수가 된다)
