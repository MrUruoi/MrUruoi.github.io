---
layout: post
title: CPU 만들기 (6)
subtitle: ALU
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 ALU
sidebar: []
---

ALU (Arithmetic and Logical Unit, 산술 논리 장치)는 산술연산과 논리연산을 담당하는 합니다.\
TD4에서는 74HC283 (SN74HC283N, 4-Bit Binary Full Adder with Fast Carry)을 사용합니다.\
(단순한 가산기이기에 ALU라고 하기에는 미묘하지만...)

![ALU](/assets/images/how_to_make_cpu_6_1.png)

## 가산 명령

ALU의 추가로 아래의 명령이 가능하게 되었습니다.

* **ADD A, Im**
* **ADD B, Im**

## 기존 명령

ALU의 추가로 가산 명령이 가능하게 되었지만 기존의 **MOV** 같은 명령에 문제가 생기는데 Im을 0000으로 설정함으로써 문제 해결이 가능합니다.\
즉, **MOV A, B**는 **A ← B + 0000(Im)** 와 같습니다.

비슷한 문제로 **MOV A, Im**가 있습니다.\
데이터 셀렉터(74HC153)의 출력이 Im에 가산되는 문제가 생기는데, 이 문제는 D레지스터(74HC161)의 0000으로 고정시키는 방법을 택했습니다.

## 플래그

TD4의 플래그는 C(캐리 플래그) 하나입니다.\
74HC283의 캐리 출력(C4)을 그대로 사용합니다.\
캐리플래그는 74HC74(SN74HC74N, Dual D-Type Positive-Edge-Triggered Flip-Flop with Clear and Preset)를 사용합니다.

## 생략한 것

어디까지나 CPU의 기본적인 구조와 원리를 이해하기 위한 목적이기에 자세한 내용은 생략했습니다.\
책에는 아래의 내용이 소개되어 있습니다.

* 반가산기와 전가산기의 설명
* 연산명령 이의의 플래그 로드