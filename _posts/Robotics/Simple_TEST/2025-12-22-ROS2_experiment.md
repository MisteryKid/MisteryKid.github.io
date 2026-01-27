---
title: ROS2 experiment_1
author: Chaewon Kim
date: 2025-12-22
category: Experiment
layout: post
---

아래의 명령어를 통해 성능을 분석해보자. 
```
htop 
```

실험환경 조성
1. vscode와 terminator를 제외한 모든 창은 꺼주기 (아니 여기 타자치는 순간에도 코어가 급발진을...;;)
2. 일을 시켰을 때 코어와 메모리, 스레드가 어떻게 동작하는지 관찰하기 
3. 작은 일부터 큰 일 순으로 테스트 진행 


## 아무것도 실행하지 않았을 때의 모습 
![image](../assets/nothing_exe.png)
Linux OS 자체가 기본적으로 점유하고 있는 자원

1. CPU 영역 
   1. 주요 점유 프로세스 
      1. gnome-shell(CPU 20.4%, MEM 1.2%)
      2. firefox(CPU 11.2%, MEM 1.1%)
         1. 브라우저 적당히 열어야겠다. 
         2. 새로고침할 때 코어 사용량 잠깐 올라갓다 내려감(대략 10% 정도)
2. 메모리
   1. 전체 62.6G에서 5.31G 사용중 -> 나중에 이값 빼야 실제 애플리케이션 순수 메모리량 알 듯 하다. 
   2. fireFox 창 두개 끄니까 4.78까지 떨어짐 

```
 task: 175, 1230 thr;
 1 running 
```
현재 메모리에 로드되어있는 독립적인 프로세스 175개
** 175개의 프로세스 내에 총 1230개의 스레드 쪼개서 운영중 **

ros2는 통신을 위해 기본적으로 스레드를 많이 생성하므로 thr가 많음 

전체 1230개의 스레드 중 1ms에 실제로 cpu코어를 붙잡고 계산하는 스레드 수는 1개 


다시 test 진행
이번에는 위의 실험환경대로 세팅 후 진행 
아무것도 실행을 하지 m않고 vscode와 terminaotr 화면 3개를 띄우고 있을 때 코어는 다음과 같은 모습을 보였음 

![image](../assets/nothing2_exe.png)


cpu core 사용량이 1%에 근접중임
메모리 사용량은 3.17G/62.6G


Tasks: 156, 739 thr;
1 running
=> ** 멀티 스레드 진행 중  **


----

## Talker와 Listener

```
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_py listener
```

case.talker 

![image](../assets/talker.png)

해설 
1. CPU 영역 
   1. 32개의 코어가 멀티프로세싱 중
      현재 모든 코어가 8~14% 정도 골구로 일하는 중 
   2. ** 이는 운영체제가 여러 코어에 부하를 분산시켜 관리하고 있음을 의미 **
2. 메모리 및 부하 
   1. Mem

case. listener 
![image](../assets/listener.png)

Talker의 경우 cpu와 mem 사용량이 0.0%로 찍히며 가끔 cpu 가 0.7%를 찍는다. 
Listener의 경우 mem이 0.1%fmf Wlrrh dlTek. 

0.0%는 값이 너무 작아서 반올림된 결과값이므로 mem%말고 RES를 한번 확인해보자. 


만약 특정 코어에게만 일을 할당하고 싶다면 아래의 명령어 사용 
```
taskset -c 7 ros2 run demo_nodes_cpp talker
```

특정 코어에 더 많은 부하를 주고 싶어서 간단한 코드 작성 후 실행 
'''
#nav2_ws/fast_talk 실행
#데이터 크기를 키울 수록 부하 커짐 
taskset -c 7 python3 fast_talker.py
'''
그 결과 다른 코어의 점유율이 0~1%일때 코어 7은 혼자 4% 점유율을 보이고 있었음 
msg.data = 'A'*5000 일 때에는 점유율이 4%였지만 
100,000으로 올리니 점유율 혼자 60%찍는 코어7

![image](../assets/Fast_serial_initial_send.png)
사진에서는 70%을 넘겼는데 이건 캡쳐한 순간에 생긴 오버헤드임




## 이미지 전송 
실제 카메라 대신 TURTLEBOT 이미지를 생성하여 송출하는 모드이다. 
이미지 전송에 어느정도의 데이터 부하를 주는지 확인해보자. 

```
ros2 run image_tools cam2image --ros-args -p burger_mode:=true
ros2 run image_tools showimage
```


![image](../assets/Image_send.png)

그림에서 볼 수 있다 싶이 core가 급발진 하는 것을 볼 수 있다. 

```
ros2 topic bw /image Subscribed to [/image]
7.08 MB/s from 30 messages
	Message size mean: 0.23 MB min: 0.23 MB max: 0.23 MB

7.11 MB/s from 61 messages
	Message size mean: 0.23 MB min: 0.23 MB max: 0.23 MB

7.05 MB/s from 91 messages
	Message size mean: 0.23 MB min: 0.23 MB max: 0.23 MB

7.02 MB/s from 100 messages
	Message size mean: 0.23 MB min: 0.23 MB max: 0.23 MB

```

위의 명령어로 데이터 대역폭을 확인한 결과 다음과 같이 해석할 수 있다. 



<div class="table-wrapper" markdown="block">

|Bandwidth|Message size|Sample Count|
|:-:|:-:|:-:|
|7.00 MB/s|0.23 MB|100 messages|
|초당 약 7MB의 데이터 발행 | 이미지 frame의 크기가 230KB | 최근 100개 메세지 기준으로 계산 |

</div>

데이터를 통해 역으로 계산해 보면 이 노드가 얼마나 빠르게 일하고 있는지 알 수 있다. 

 7.00 MB/s÷0.23 MB/frame≈30.4 FPS

즉, 현재 cam2image 노드는 초당 약 30장의 이미지를 쉴 새 없이 찍어서 보내고 있다.

또 CPU점유율을 내림차순 정렬한 결과 /usr/bin/gnome-shell이 상위권을 모두 차지하고 있는 것을 보아 이미지 통신 그 자체보다는 화면에 랜더링해서 보여주는게 더 오버헤드가 크다는 것을 알 수 있다. 


----
제미나이에게 물어본 해설 

프로파일링 관점에서의 의미 (왜 중요할까?)

이 7.00 MB/s라는 숫자는 단순히 데이터 양이 아니라 CPU와 메모리가 감당해야 할 업무량을 의미합니다.

    CPU 부하: 0.23MB 데이터를 초당 30번씩 복사하고, ROS2 표준 형식으로 포장(Serialization)해서 전달해야 합니다. 아까 talker가 보냈던 "Hello World"는 수 바이트(Bytes)에 불과했지만, 지금은 수만 배 더 많은 연산을 하고 있는 것입니다.

    메모리(RAM) 부하: 시스템은 이 0.23MB짜리 데이터를 담기 위해 메모리 공간을 계속 할당하고 해제하거나, 버퍼에 유지해야 합니다. htop에서 RES 수치가 아까보다 높게 유지되는 이유가 바로 이것입니다.

    DDS 오버헤드: ROS2의 통신 미들웨어(DDS)는 이 7MB/s의 데이터를 유실 없이 보내기 위해 내부적으로 스레드를 바쁘게 돌립니다. 32개의 코어 중 특정 코어들이 이 통신을 처리하느라 점유율이 올라갔을 것입니다.
----


## Gazebo

지금 가제보 말고도 vscode, firefox, terminator 4대를 동시에 켜두고 있어서 부하가 가제보 부하 + a 로 들어오는중
로봇 소환 대수 별로 부하 차이가 있는지 확인해보자. !!

랜더링할때 부하가 많이 걸리니 현재 모니터 1대의 절반만 차지하도록 창을 켜두자. 
gazebo 창 커지면 부하 커짐 

   창이 작을 때: 그래픽 카드가 그려야 할 픽셀 수가 적고, CPU가 GPU에게 "이거 그려줘"라고 명령(Draw Call)을 내리는 횟수나 관리 부하가 줄어듭니다.

|터틀봇 대수 |:-:|코어 할당량 평균(일단 눈대중으로)| tasks | thr |
|1대|:-:|20% 후반 | 183| 1532 |
|2대|:-:|20% 중후반| 184 |1542|
|3대|:-:|30% 초반 | 185 | 1560|
|4대|:-:|20% 후반 ~ 30% | 186 | 1570|


```
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
ros2 launch turtlebot3_gazebo multi_robot.launch.py
# 여기서 코드 수정 
```

로봇 대수가 많아질 수록 task와 thread가 많아지지만 코어 점유율에는 큰 변화가 있지는 않다. 

--- 
젬나이 해설
32코어의 "압도적 여유" (계산의 함정)

사용자님이 보시는 **30%**라는 수치는 전체 32개 코어의 평균입니다. 이걸 '코어 개수'로 환산해보면 놀라운 사실이 숨어있습니다.

    평균 30% 사용 시: 32 cores×0.3=9.6 cores (약 10개의 코어가 풀가동 중)

    로봇 1대 → 4대 변화: 태스크(Task)는 3개, 스레드(Thread)는 약 40개 정도 늘어났습니다. 하지만 이미 시스템에는 1,500개가 넘는 스레드가 돌아가고 있습니다.

    결론: 1,500명 부대원에게 40명의 신병이 추가된 수준이라, 전체 점유율 30% 내에서는 그 변화가 **'오차 범위'**처럼 보일 정도로 미미한 것입니다. 32코어 시스템은 로봇 몇 대 추가되는 것 정도로는 "간에 기별도 안 가는" 상태인 거죠.

---