---
title: About
author: Chaewon Kim
date: 2025-12-22
layout: post
permalink: /about/ 
---

<style>
    .timeline-container {
        max-width: 600px;
        margin: 40px auto;
        font-family: 'Pretendard', sans-serif;
    }
    .timeline-item {
        position: relative;
        padding-left: 40px;
        margin-bottom: 30px;
        border-left: 2px solid #e9ecef; /* 세로선 */
    }
    .timeline-item::before {
        content: '';
        position: absolute;
        left: -7px; /* 선 위에 점 맞추기 */
        top: 5px;
        width: 12px;
        height: 12px;
        background-color: #dee2e6;
        border-radius: 50%;
        border: 2px solid #fff;
    }
    .timeline-date {
        font-size: 14px;
        font-weight: 600;
        color: #868e96;
        margin-bottom: 5px;
    }
    .timeline-content {
        font-size: 16px;
        color: #212529;
        font-weight: 500;
    }
    /* 현재 진행 중인 항목 강조 */
    .timeline-item.active::before {
        background-color: #339af0;
    }
    .timeline-item.active .timeline-date {
        color: #339af0;
    }
</style>

<div class="about-profile" style="margin-bottom: 60px; font-family: 'Pretendard', sans-serif;">
    <h1 style="font-size: 2.2rem; font-weight: 800; color: #212529; margin-bottom: 20px; letter-spacing: -1px;">
        시스템 관점에서 로봇의 미래를 고민하는 <br>
        <span style="color: #339af0;">컴퓨터공학도 김채원</span>입니다.
    </h1>

    <div style="background: #f8f9fa; padding: 25px; border-radius: 12px; border-left: 5px solid #339af0;">
        <p style="margin: 0; font-size: 1.1rem; line-height: 1.8; color: #495057;">
            🎓 <strong>동국대학교 AI융합대학 컴퓨터공학전공</strong> (4학년 재학)<br>
            🔍 <strong>Current Focus:</strong> ROS 2 아키텍처를 시스템 관점에서 이해하기 위해 공부하고 있습니다. 운영체제의 핵심 개념(Scheduling, IPC)이 로봇 시스템 위에서 어떻게 구현되는지 코드를 뜯어보며 그 간극을 메워가는 중입니다.
        </p>
    </div>

    <div style="margin-top: 30px; display: flex; flex-wrap: wrap; gap: 10px;">
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">System Programming</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">ROS 2 Internals</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">Linux Kernel</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">Zero Copy</span>
    </div>
</div>


<div class="timeline-container">
    <h3 style="margin-left: -40px; color: #adb5bd; margin-bottom: 20px;">2023 - 2025</h3>

    <div class="timeline-item">
        <div class="timeline-date">2023.03</div>
        <div class="timeline-content">동국대학교 입학 🎓</div>
    </div>

    <div class="timeline-item active">
        <div class="timeline-date">2025.12</div>
        <div class="timeline-content"> NOSLAB 인턴 시작 🤖</div>
    </div>
</div>

<section style="margin-top: 60px;">
    <h3 style="border-bottom: 2px solid #339af0; padding-bottom: 8px; display: inline-block;">Current Learning Path</h3>
    <div style="margin-top: 20px; line-height: 2;">
        <p style="color: #495057;">시스템 관점에서 ROS 2를 이해하기 위해 다음 단계들을 하나씩 밟아가고 있습니다.</p>
        <ul style="list-style-type: '📂 '; padding-left: 20px;">
            <li><strong>DDS 미들웨어 분석</strong>: DDS에 따른 성능 비교 실험</li>
            <li><strong>RCLCPP 내부 구조</strong>: 노드 실행 및 콜백 스케줄링 알고리즘 파악</li>
        </ul>
    </div>
</section>


<section style="margin-top: 50px; font-family: 'Pretendard', sans-serif;">
    <h3 style="border-bottom: 2px solid #339af0; padding-bottom: 8px; display: inline-block; color: #212529;">Deep Dive: ROS 2 Internals</h3>
    
    <div style="margin-top: 20px; line-height: 1.8;">
        <p style="color: #495057; font-size: 16px;">
            단순히 API를 사용하는 것을 넘어, <strong>컴퓨터공학적 관점</strong>에서 ROS 2의 성능 한계를 극복하기 위해 아래 주제들을 심도 있게 분석하고 있습니다.
        </p>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 25px;">
            <div style="background: #ffffff; border: 1px solid #e9ecef; padding: 20px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.02);">
                <div style="font-size: 24px; margin-bottom: 10px;">⚙️</div>
                <h4 style="margin: 0 0 10px 0; color: #339af0;">Executor Scheduling</h4>
                <p style="margin: 0; font-size: 14px; color: #868e96;">
                    rclcpp Executor의 소스 코드를 분석하며 콜백이 스케줄링되는 메커니즘을 공부합니다. 특히 멀티 스레드 환경에서 결정론적(Deterministic) 실행을 보장하는 방법에 관심이 많습니다.
                </p>
            </div>

            <div style="background: #ffffff; border: 1px solid #e9ecef; padding: 20px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.02);">
                <div style="font-size: 24px; margin-bottom: 10px;">🚀</div>
                <h4 style="margin: 0 0 10px 0; color: #339af0;">Zero-Copy Mechanism</h4>
                <p style="margin: 0; font-size: 14px; color: #868e96;">
                    대용량 데이터 전송 시 발생하는 오버헤드를 줄이기 위해 Shared Memory 기반의 Zero-copy가 왜 필수적인지, 그리고 이를 통해 시스템 자원을 효율적으로 사용하는 구조를 연구합니다.
                </p>
            </div>
        </div>
    </div>
</section>


<section style="margin-top: 60px; font-family: 'Pretendard', sans-serif;">
    <h3 style="border-bottom: 2px solid #339af0; padding-bottom: 8px; display: inline-block; color: #212529;">2026 Focus & Goals</h3>
    
    <div style="margin-top: 25px; background: #f8f9fa; padding: 30px; border-radius: 15px; border: 1px solid #e9ecef;">
        <div style="display: grid; gap: 20px;">
            
            <div style="display: flex; align-items: flex-start; gap: 15px; background: #fff; padding: 20px; border-radius: 12px; box-shadow: 0 2px 4px rgba(0,0,0,0.03);">
                <div style="background: #e7f5ff; color: #339af0; width: 35px; height: 35px; display: flex; align-items: center; justify-content: center; border-radius: 50%; font-weight: 800; flex-shrink: 0;">1</div>
                <div>
                    <strong style="font-size: 17px; color: #212529;">데이터로 증명하는 시스템 최적화 (국문 논문)</strong>
                    <p style="margin: 8px 0 0 0; font-size: 14.5px; color: #495057; line-height: 1.6;">
                        ROS 2 통신 메커니즘을 심도 있게 분석하여, 시스템 성능의 임계점을 보여주는 <strong>'의미 있는 그래프 하나'</strong>를 도출하고 이를 바탕으로 KCI 등재지 혹은 학술대회 논문 1편 게재를 목표로 합니다.
                    </p>
                </div>
            </div>

            <div style="display: flex; align-items: flex-start; gap: 15px; background: #fff; padding: 20px; border-radius: 12px; box-shadow: 0 2px 4px rgba(0,0,0,0.03);">
                <div style="background: #e7f5ff; color: #339af0; width: 35px; height: 35px; display: flex; align-items: center; justify-content: center; border-radius: 50%; font-weight: 800; flex-shrink: 0;">2</div>
                <div>
                    <strong style="font-size: 17px; color: #212529;">커널 레벨 프로파일링 숙달</strong>
                    <p style="margin: 8px 0 0 0; font-size: 14.5px; color: #495057; line-height: 1.6;">
                        LTTng 및 <code>ros2_tracing</code>을 활용하여 마이크로초($\mu s$) 단위의 시스템 레이턴시를 정교하게 측정하고, OS 스케줄링이 로봇 소프트웨어에 미치는 영향을 코드 레벨에서 추적합니다.
                    </p>
                </div>
            </div>

            <div style="display: flex; align-items: flex-start; gap: 15px; background: #fff; padding: 20px; border-radius: 12px; box-shadow: 0 2px 4px rgba(0,0,0,0.03);">
                <div style="background: #e7f5ff; color: #339af0; width: 35px; height: 35px; display: flex; align-items: center; justify-content: center; border-radius: 50%; font-weight: 800; flex-shrink: 0;">3</div>
                <div>
                    <strong style="font-size: 17px; color: #212529;">기술 공유의 습관화</strong>
                    <p style="margin: 8px 0 0 0; font-size: 14.5px; color: #495057; line-height: 1.6;">
                        복잡한 시스템 프로그래밍 개념을 나만의 언어로 정리하여 월 2회 이상 기술 블로그에 기록합니다. '공유를 위한 공부'를 통해 지식의 빈틈을 메우고 커뮤니티와 함께 성장합니다.
                    </p>
                </div>
            </div>

        </div>
    </div>
</section>



<section style="margin-top: 60px; font-family: 'Pretendard', sans-serif;">
    <h3 style="border-bottom: 2px solid #f1f3f5; padding-bottom: 10px; color: #212529;">Get in Touch</h3>
    
    <div style="display: flex; flex-direction: column; gap: 15px; margin-top: 25px;">
        <div style="display: flex; align-items: center; gap: 12px;">
            <span style="font-size: 20px;">🏫</span>
            <span style="font-size: 16px; color: #495057;">
                Member of <a href="https://noslab.github.io/" target="_blank" style="color: #339af0; text-decoration: none; font-weight: 700; border-bottom: 1px solid #339af0;">Dongguk Univ. NOSLAB</a> (Next-generation Operating Systems Lab)
            </span>
        </div>

        <div style="display: flex; align-items: center; gap: 12px;">
            <span style="font-size: 20px;">✉️</span>
            <a href="mailto:your_email@gmail.com" style="font-size: 16px; color: #339af0; text-decoration: none; font-weight: 500;">
                abade3@dgu.ac.kr
            </a>
        </div>

        <div style="display: flex; align-items: center; gap: 12px;">
            <span style="font-size: 20px;">🐙</span>
            <a href="https://github.com/misterykid" target="_blank" style="font-size: 16px; color: #339af0; text-decoration: none; font-weight: 500;">
                github.com/misterykid
            </a>
        </div>
    </div>
</section>