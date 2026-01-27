---
layout: home
title: MisteryKid의 블로그
subtitle: 지킬로 만드는 나의 첫 개발 블로그
---


### 안녕하세요! 👋
이곳은 저의 study 기록을 담는 공간입니다.

현재 테마를 설정 중이며, 앞으로 유익한 정보들을 공유할 예정입니다.

#### 최근 포스트


### 🚀 주요 카테고리
* [ROS2 연구실]({{ site.baseurl }}/category/ros2)
* [실시간 시스템 분석]({{ site.baseurl }}/category/paper)

---
### 📌 최신 게시글
{% for post in site.posts limit:5 %}
* [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}


### 🛠 Tech Stack
![ROS2](https://img.shields.io/badge/ros2-%2322314E.svg?style=for-the-badge&logo=ros&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)


