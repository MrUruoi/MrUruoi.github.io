---
layout: post
title: CPU 만들기 (9)
subtitle: 명령 디코드
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 Instruction_decoder
sidebar: []
---

명령을 지시로 변환하는 회로가 `명령 디코더`라고 할 수 있습니다.\
변환 회로라고 해도 기본적으로 단순한 AND나 OR 게이트의 집합입니다.

## 명령 실행의 흐름

명령을 가져오는 과정인데 `Instruction Fetch`라고도 합니다.

* 실행할 명령의 주소는 프로그램 카운터가 가리키고 있습니다.
* 이 주소를 ROM에 출력하면, ROM은 지정된 주소에 저장된 명령을 반환합니다.
* CPU가 실행할 명령을 확인
* 명령의 하위 4비트는 이미디어트 데이터로 ALU로 전송됩니다.
* 명령의 상위 4비트는 오퍼레이션 코드이지만, 지금은 사용되지 않고 있습니다.

## 실행부의 동작

*　SELECT A와 SELECT B의 신호에 의해 4채널 데이터 셀렉터가 레지스터를 선택하여 ALU로 보냅니다.
* ALU가 연산 후 모든 레지스터에 연산결과를 보냅니다.
* <span style="text-decoration: overline;">LOAD0</span> ~ <span style="text-decoration: overline;">LOAD3</span> 신호에 의해 각 레지스터(출력 포트와 프로그램 카운터를 포함)의 유지 또는 로드가 결정됩니다. 즉, 전송 대상입니다.
* 다음 클록에 실행(쓰기, 즉 전송)하기만 하면 됩니다.

## 명령 디코드의 Input과 Output

* Input: 오퍼레이션 코드 4bit와 C플래그
* Output: SELECT A, SELECT B, <span style="text-decoration: overline;">LOAD0</span> ~ <span style="text-decoration: overline;">LOAD3</span>

### <span style="text-decoration: overline;">LOAD0</span> ~ <span style="text-decoration: overline;">LOAD3</span>

 **L: 로드**\
 **H: 유지**\
(상세 내용은 74HC161의 진리표를 확인) 

### SELECT A, SELECT B

| SELECT B | SELECT A | 동작 |
|--|--|--|
| L | L | 입력C0 (A레지스터)가 출력 |
| L | H | 입력C1 (B레지스터)가 출력 |
| H | L | 입력C2 (입력포트)가 출력 |
| H | H | 입력C3 (0000)가 출력 |

(상세 내용은 74HC153의 진리표를 확인) 

### 예시

**명령 포멧**

| bit7 |bit6 | bit5 | bit4 | bit3 | bit2 | bit1 | bit0 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 1 | 1 | Im ||||

**상세**: Im을 A레지스터에 전송

**C플래그**\
실행시: 이 명령은 C플래그의 영향을 받지 않습니다.\
실행후: 반드시 0이 됩니다.

**실행부의 지시**

| SELECT B | SELECT A | <span style="text-decoration: overline;">LOAD0</span> | <span style="text-decoration: overline;">LOAD1</span> | <span style="text-decoration: overline;">LOAD2</span> | <span style="text-decoration: overline;">LOAD3</span> |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| H | H | L | H | H | H |

## 명령 일람

| 명령 | OP3 | OP2 | OP1 | OP0 | C Flag | SELECT B | SELECT A | <span style="text-decoration: overline;">LOAD0</span> | <span style="text-decoration: overline;">LOAD1</span> | <span style="text-decoration: overline;">LOAD2</span> | <span style="text-decoration: overline;">LOAD3</span> | 
| ADD A, Im | L | L | L | L | X | L | L | L | H | H | H |
| MOV A, B | L | L | L | H | X | L | H | L | H | H | H |
| IN A | L | L | H | L | X | H | L | L | H | H | H |
| MOV A, Im | L | L | H | H | X | H | H | L | H | H | H |
| MOB B, A | L | H | L | L | X | L | L | H | L | H | H |
| ADD B, Im | L | H | L | H | X | L | H | H | L | H | H |
| IN B| L | H | H | L | X | L | H | L | H | H | H |
| MOV B, Im| L | H | H | H | X | H | H | H | L | H | H |
| OUT B | H | L | L | H | X | L | H | H | H | L | H |
| OUT Im | H | L | H | H | X | H | H | H | H | L | H |
| JNC (C = 0) | H | H | H | L | L | H | H | H | H | H | L |
| JNC (C = 1) | H | H | H | L | H | X | X | H | H | H | H |
| JMP | H | H | H | H | X | H | H | H | H | H | L |
 
 \* 출력의 X는 H, L 아무거나 출력해도 괜찮다는 의미 

## 회로

![Decoder](/assets/images/how_to_make_cpu_9_1.png)

실제 사용한 IC는 아래 2개입니다.\
OR X 4: 74HC32 (SN74HC32N, Quadruple 2-Input Positive-OR Gate)\
3입력NAND X 3: 74HC10 (SN74HC10N, Triple 3-Input Positive-NAND Gate)

## 완성



## 생략한 것

어디까지나 CPU의 기본적인 구조와 원리를 이해하기 위한 목적이기에 자세한 내용은 생략했습니다.\
책에는 아래의 내용이 소개되어 있습니다.

* 진리표의 단순화
* 드모르간의 법칙
* 카르노 맵
