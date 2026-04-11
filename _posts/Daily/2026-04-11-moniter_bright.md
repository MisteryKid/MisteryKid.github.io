---
title: 우분투 22.04 듀얼 모니터 화면 밝기 조절 스크립트 만들기
author: Chaewon Kim
date: 2026-03-01
category: Daily
layout: post
---

## xrandr를 이용해서 모니터 밝기 조절하기
- 화면 밝기가 너무 밝아서 장시간 공부가 불가 및 눈이 아픔
- 아래와 같은 방법으로 해결 

### 설치 환경
- Ubuntu 22.04 LTS
- 삼성 모니터 2대 (듀얼 모니터)
- 사용 도구: xrandr (우분투 기본 내장)

### xrandr 이란
- xrandr(X Resize and Rotate)은 리눅스 X 윈도우 시스템에서 디스플레이의 해상도, 방향, 밝기 등을 설정하는 기본 도구
- 소프트웨어적으로 화면 밝기 조절 가능


### xrandr 설치
```shell
sudo apt update
sudo apt install x11-xserver-utils

```

### 모니터 이름 확인하기
내 컴퓨터에 연결된 모니터의 '시스템 상 이름'을 확인

```shell
xrandr | grep " connected"
```
아래와 같이 출력이 나옴
![img](</assets/img/Daily/connect_monitor.png.png>)

위 이름 메모장에 적어두기

### 밝기 조절 스크립트 파일 만들기

나는 홈 화면에서 바로 조작할 수 있도록 ~/ 경로에 생성

```shell
# 이름 변경 가능 
vim set-bright.sh
```

아래와 같이 코드 작성
```shell
#!/bin/bash

# 1. 입력받은 밝기 값을 변수에 저장 (입력값이 없으면 기본값 0.8 사용)
BRIGHTNESS=${1:-0.8}

# 2. 안전장치: 밝기를 0으로 설정하는 것 방지
if [ "$BRIGHTNESS" == "0" ] || [ "$BRIGHTNESS" == "0.0" ]; then
    echo "╯°□°）╯︵ ┻━┻ 경고: 밝기를 0으로 설정하면 화면이 보이지 않습니다!"
    echo "설정이 취소되었습니다."
    exit 1
fi

# 3. xrandr 명령어로 밝기 적용 (본인 모니터 이름으로 수정 필수!)
xrandr --output HDMI-0 --brightness $BRIGHTNESS
xrandr --output DP-0 --brightness $BRIGHTNESS

# 4. 완료 메시지 출력
echo "( ˘▽˘)っ 화면 밝기가 $BRIGHTNESS(으)로 변경되었습니다."

```

### 스크립트에 실행 권한 주기
```shell
chmod +x set-bright.sh
```

그러면 파일이 흰색에서 초록색으로 바뀔 것이다.

### 스크립트 실행하기
```shell
# 기본 실행
./set-bright.sh

# 밝기 100% 설정
./set-bright.sh 1

# 좀 어둡게 하고 싶을 때
./set-bright.sh 0.5
```

매개변수값을 잘 조정해서 화면 밝기 조절이 가능하다. 