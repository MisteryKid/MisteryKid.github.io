---
title: ROS2 experiment
author: Chaewon Kim
date: 2025-12-22
category: Jekyll
layout: post
---

## 1. Talker와 Listener의 자원 사용량 살펴보기 

case. talker 

![alt text](talker.png)

case. listener 
![alt text](listener.png)

Talker의 경우 cpu와 mem 사용량이 0.0%로 찍히며 가끔 cpu 가 0.7%를 찍는다. 
Listener의 경우 mem이 0.1%fmf Wlrrh dlTek. 

0.0%는 값이 너무 작아서 반올림된 결과값이므로 mem%말고 RES를 한번 확인해보자. 