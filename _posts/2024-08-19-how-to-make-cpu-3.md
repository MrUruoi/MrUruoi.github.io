---
layout: post
title: CPU 만들기 (3)
subtitle: ROM
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 ROM
sidebar: []
---

`ROM` Read Only Memory의 약자로 수정이나 삭제가 불가능한 기억장치를 가리킵니다.(역사적인? 이유로 Read Only지만 현재는 수정 가능)\
여기서는 프로그램용으로 DIP스위치를 이용해서 ROM(DIP Switch, 8 Position, SPST)을 제작합니다.

![ROM](/assets/images/how_to_make_cpu_3_1.png)

## ROM으로써 필요한 기능

필요한 기능이라고 해도 어떠한 데이터(프로그램)를 가지고 있을 뿐, CPU가 그 데이터를 사용합니다.\
CPU가 ROM에게 "n번지 데이터 보내줘" 라는 식인데, 여기서 n번지를 지정하는 신호를 `Address bus`, 데이터를 보내는 신호를 `Data bus` 라고 합니다.

## 8bit 출력

1bit ROM은 간단히 스위치 ON OFF로 표현 가능합니다.\
현재 만드는 CPU의 명령은 8bit 이기에 8bit 표현이 가능한 DIP스위치를 사용하고,\
16스텝까지의 프로그램 실행이 가능하도록, 16개의 DIP스위치를 사용합니다.

## 어드레스 선택

n번지를 어떻게 지정할 지의 문제인데, 여기서는 `74HC154`(SN74HC154NT, 4-Line to 16-Line Decoder / Demultiplexer)를 사용합니다.\
간단히 설명하면, Input의 A~D에 2진수를 입력하면, Output의 Ȳ0~Ȳ15가 순서대로 L이 됩니다. (여기서는 선택되면 L출력)\
(자세한 설명은 데이터시트를 참고)

| 번지 (이진수) | 선택 |
|--|--|
| 0 (0000) | 0 |
| 1 (0001) | 1 |
| 2 (0010) | 2 |
| 3 (0011) | 3 |
|...||
| 15 (1111) | 15 |

## Data bus의 인버터

Data bus의 인버터로 `74HC540`(SN74HC540N, Octal Buffer and Line Driver with 3-State Outputs)를 사용합니다.

## 생략한 것

어디까지나 CPU의 기본적인 구조와 원리를 이해하기 위한 목적이기에 자세한 내용은 생략했습니다.\
책에는 아래의 내용이 소개되어 있습니다.

* 비트수가 많을 때의 문제점
* 다이오드의 사용 이유
* 74HC154의 내부
