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
