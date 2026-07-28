---
title: "[RTAS'26] Anytime ROS 2, Timely Task Completion in Non-Preemptive Robotic Systems"
author: Chaewon Kim
date: 2026-07-28
categories: [Paper, ROS2]
layout: post
---

## 작성중 

> **논문 링크:** [https://ieeexplore.ieee.org/abstract/document/11558386](https://ieeexplore.ieee.org/abstract/document/11558386)  


## 📌 TL;DR (한 줄 요약)
- ROS 2의 User space scedulaer인 Executor는 비선점형 알고리즘을 지니고 있어 AI와 같인 긴 연산시간을 가진 task가 있을 경우, 다른 작업들이 밀리는 현상 관측 
- 이는 자율주행과 같은 Real-time System에서 중요한 작업이 밀릴 경우 사고를 일으킬 수 있음 
- 긴 연산시간을 가진 작업을 subtask로 작게 쪼개서 각 단계 사이에 스케줄링 포인트를 삽입하는 Anytime 알고리즘 기법을 제안
- 이를 통해 AI 연산 중 다른 작업이 점유할 수 있도록 구성 

---

## 1. Background & Motivation (배경 및 동기)
- **어떤 문제를 풀고자 하는가?** 
  - (예시) 자율주행 환경에서 악천후 시 카메라 센서의 인지 능력이 급격히 떨어지는 문제.
- **기존 연구들의 한계점은 무엇인가?** 
  - (예시) 기존의 센서 퓨전 방식은 계산량이 너무 많아 실시간(Real-time) 처리에 부적합했음.

## 2. Key Idea / Methodology (핵심 아이디어 및 방법론)
- **저자들이 제안하는 해결 방법(알고리즘, 구조 등)은 무엇인가?**
  - 핵심 알고리즘 흐름이나 아키텍처의 주요 구성 요소를 객관적으로 설명합니다.
  - 수학적 모델링이나 Loss Function의 핵심 변화를 수식과 함께 적어두면 좋습니다.
- *필요하다면 논문 내 핵심 그림이나 Mermaid 다이어그램을 첨부하세요.*

## 3. Evaluation / Results (실험 및 결과)
- **어떤 데이터셋/환경에서 실험을 진행했는가?** 
  - (예시) nuScenes 데이터셋, ROS2 시뮬레이터 (Gazebo)
- **주요 성능 지표(Metrics)는 무엇이고, 기존 방식 대비 얼마나 개선되었는가?**
  - (예시) 기존 Baseline 모델 대비 mAP가 3% 상승하였으며, FPS는 15에서 30으로 증가함.

## 4. Conclusion (결론)
- **논문의 요약:** 저자들이 논문에서 제시하는 결론과 한계점(Limitations).
  - (예시) 본 논문은 경량화된 센서 퓨전 기법을 통해 실시간 성능을 확보함. 그러나 야간 환경에서의 테스트는 충분히 이루어지지 않음.
- **Future Work:** 논문에서 언급한 향후 연구 방향이나 개선 가능성.

---

### 💡 (선택) Code & Implementation
- **공식 Github:** [https://github.com/example/repo](https://github.com/example/repo)
- **구현 특징:** 
  - (예시) PyTorch 기반으로 작성되었으며, ROS2 노드 래퍼(Wrapper)를 함께 제공하여 실제 로봇에 바로 탑재해 볼 수 있음.
