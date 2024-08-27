---
layout: post
title: CPU 만들기 (8)
subtitle: I/O
author: gonayun
categories: etc.
tags: CPU cpuの創りかた TD4 I/O
sidebar: []
---

I/O라고 하면 어렵게 들릴 수 있지만, 1과 0을 입출력하는 것 뿐입니다.\
예를 들어, LED를 연결해서 출력이 1001이면 점등・소등・소등・점등 하는 식의 방법도 생각할 수 있습니다.

## 출력 포트

TD4에서는 C레지스터(74HC161)를 출력용으로 사용합니다.\
여기에 LED를 연결했습니다.

## 입력 포트

입력 포트는 DIP 스위치(SW DIP-4)를 사용합니다.\
4개의 스위치이므로 역시나 4bit 입력입니다.

![I/O](/assets/images/how_to_make_cpu_8_1.png)