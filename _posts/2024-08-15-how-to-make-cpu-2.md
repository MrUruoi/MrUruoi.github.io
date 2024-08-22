---
layout: post
title: CPU 만들기 (2)
subtitle: 리셋 회로와 클럭 제너레이터
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 reset clock
sidebar: []
---

`Reset`에 의해 CPU가 시작되며, `Clock` 신호에 맞춰 하나씩 처리를 실행합니다.

## 리셋 회로

리셋 회로는 CPU를 초기화 시키는데 사용됩니다. CPU에 전원을 공급할 때도 사용되는데, 전원 공급 시 리셋 신호를 만들어는 리셋 회로를 Power on reset이라고 부른다고 합니다.

## 클럭 제너레이터

`Clock`은 간단히 말해서 초당 실행하는 작업 처리 횟수를 나타내며, `Hz` 단위로 표시합니다. 1Hz는 1초에 1번 처리를 의미합니다.\
클럭 제너레이터는 말 그대로 클럭을 만들어 주는 역할을 합니다.\
여기에서는 콘텐서와 저항을 이용했는데, 원리까지 이해할 필요는 없고 전기적 진동을 만들어 주는 무언가 정도로 이해하면 될 거 같습니다.

## 브레드 보드로 연습

사용한 IC는 74HC14 (SN74HC14N, Hex Schmitt-Trigger Inverter)
![reset_clock](/assets/images/how_to_make_cpu_2_1.png)

## 키트 조립

![reset_clock](/assets/images/how_to_make_cpu_2_2.png)

## 생략한 것

어디까지나 CPU의 기본적인 구조와 원리를 이해하기 위한 목적이기에 자세한 내용은 생략했습니다.\
책에는 아래의 내용이 소개되어 있습니다.

* 풀업 (Pull up)과 풀다운 (Pull down)
* 채터링 (chattering) 방지
* CR 필터
* 슈미트 트리거 (Schmitt trigger)
* 콘덴서에 대한 설명