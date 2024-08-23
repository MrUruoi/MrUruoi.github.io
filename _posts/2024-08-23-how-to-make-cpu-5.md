---
layout: post
title: CPU 만들기 (5)
subtitle: test
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 Fip-Flop
sidebar: []
---

## 플립플롭 (Flip-Flop)

플립플롭은 간단히 말하면 1비트 메모리입니다. TD4는 4비트의 A 레지스터와 B레지스터가 있는데, 4비트이므로 4개의 플립플롭으로 구성됩니다.

## 레지스터

레지스터용으로 74HC161 (SN74HC161N, 4-Bit Synchronous Binary Counter) 4개 사용합니다.\
(2개는 다른 용도로 사용)

## 채널 셀렉터

사용하는 IC는 74HC153 (SN74HC153N, Dual 4-Line to 1-Line Data Selector/Multiplexer) 2개 입니다.

![Resister](/assets/images/how_to_make_cpu_5_1.png)

## 생략한 것

어디까지나 CPU의 기본적인 구조와 원리를 이해하기 위한 목적이기에 자세한 내용은 생략했습니다.\
책에는 아래의 내용이 소개되어 있습니다.

* 플립플롭의 데이터 저장과 보존
* 74HC161, 