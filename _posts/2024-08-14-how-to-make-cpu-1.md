---
layout: post
title: CPU 만들기
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4
sidebar: []
---

예전에 `cpuの創りかた` (cpu 만드는 법) 이라는 도서를 구입해서 읽은 적이 있습니다.
단순히 CPU의 작동원리를 이해하기 위해 읽기만 했는데, 우연히 AliExpress 에서 DIY 키트를 판매하고 있길래 직접 만들어 보았습니다.

## 책 소개

`cpuの創りかた` 渡波 郁 (著), 직접 CPU(4bit)를 만들어 보면서, 기본적인 CPU의 구조와 동작 원리를 알 수 있는 책입니다.
직접 손으로 무언가를 만들어가면서 배우고 싶으신 분 들에게 추천드립니다.
아쉽게도 한국어 번역본은 없는 것 같네요.
![cpuの創りかた](/assets/images/how_to_make_cpu_1.png)

## 만든 것

DIY 키트를 사용해서 그다지 어렵지는 않았지만 직접 납땜도 해야하기에
도전하기에 은근히 허들이 있습니다.
![td4](/assets/images/how_to_make_cpu_2.png)

## 준비

### 구입 물품

* CPU DIY Kit TD4 (AliExpress)
* 납땜용품
  * 인두기, 땜납, 솔더위크, 팁 클리너, 니퍼, 멀티테스터
* 연습, 동작확인용
  * 브레드보드, 브레드보드용 점프 와이어세트. 브레드보드용 마이크로B USB 커넥터 DIP 키트, 3mmLED, 유니버설 기판

### 납땜 연습

* 남땜에 대한 지식이 전혀 없어기에 유튜브를 보면서 연습
* 솔더위크, 팁 클리너 사용법도 연습

### LED 점멸

* 전자회로?에 대한 지식이 전혀 없었기에, LED 점멸을 목표로 브레드 보드로 연습
* 전류, 전압, 저항에 대해 간단히 복습 (+ 옴의 법칙)
* 멀티미터 사용법도 연습

![LED](/assets/images/how_to_make_cpu_3.png)

### 디지털 회로의 기초의 기초를 공부

* 범용 IC 공부, 어디까지나 CPU제작이 목표이기에 사용할 수 있을 정도까지만 공부
* 간단한 논리 회로에 대한 이해 (NOT, AND, OR, NAND, 다입력 게이트)

![IC](/assets/images/how_to_make_cpu_4.png)

