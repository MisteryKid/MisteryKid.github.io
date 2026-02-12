---
title: About
author: Chaewon Kim
date: 2025-12-22
category: Jekyll
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
            🔍 <strong>Current Focus:</strong> ROS 2의 분산 시스템 아키텍처를 분석하고, 커널 및 미들웨어 수준에서 성능을 최적화하고 시스템적 한계를 개선하는 연구를 진행하고 있습니다.
        </p>
    </div>

    <div style="margin-top: 30px; display: flex; flex-wrap: wrap; gap: 10px;">
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">System Programming</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">ROS 2 Internals</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">Linux Kernel</span>
        <span style="border: 1px solid #339af0; color: #339af0; padding: 4px 12px; border-radius: 5px; font-size: 14px; font-weight: 600;">Distributed Systems</span>
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

