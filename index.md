---
layout: default
title: Home
---

<style>
    /* 1. GitBook 기본 사이드바 숨기기 (메인에서만) */
    .book-summary { display: none !important; }
    .book-body { left: 0 !important; width: 100% !important; }
    .book-header { display: none !important; } /* 기존 헤더 숨김 */

    /* 2. 전체 레이아웃 잡기 */
    .daangn-container {
        max-width: 720px; /* 미디엄/당근 블로그의 가독성 최적 너비 */
        margin: 0 auto;
        padding: 0 20px;
        font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
        color: #212529;
    }

    /* 3. 헤더 스타일 */
    .daangn-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 40px 0 60px 0;
    }
    .daangn-logo {
        font-size: 24px;
        font-weight: 800;
        color: #ff6f0f; /* 당근마켓 주황색 포인트 */
        text-decoration: none;
    }
    .daangn-nav a {
        margin-left: 20px;
        color: #868e96;
        text-decoration: none;
        font-size: 15px;
        font-weight: 500;
    }
    .daangn-nav a:hover { color: #212529; }

    /* 4. 포스트 리스트 스타일 (핵심!) */
    .post-item {
        display: flex;
        justify-content: space-between;
        margin-bottom: 48px;
        border-bottom: 1px solid #f1f3f5;
        padding-bottom: 48px;
    }
    .post-content {
        flex: 1;
        padding-right: 24px;
    }
    .post-title {
        font-size: 22px;
        font-weight: 700;
        margin-bottom: 8px;
        line-height: 1.4;
        display: block;
        text-decoration: none;
        color: #212529;
    }
    .post-excerpt {
        font-size: 16px;
        color: #495057;
        line-height: 1.6;
        margin-bottom: 12px;
        display: -webkit-box;
        -webkit-line-clamp: 3; /* 3줄 넘어가면 ... 처리 */
        -webkit-box-orient: vertical;
        overflow: hidden;
    }
    .post-meta {
        font-size: 13px;
        color: #868e96;
    }
    
    /* 썸네일 이미지 (오른쪽에 작게 배치) */
    .post-thumbnail {
        width: 120px;
        height: 120px;
        background-color: #f8f9fa;
        border-radius: 4px;
        overflow: hidden;
        flex-shrink: 0; /* 이미지 크기 줄어들지 않게 고정 */
    }
    .post-thumbnail img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    /* 모바일 대응 */
    @media (max-width: 768px) {
        .post-item { flex-direction: column-reverse; }
        .post-thumbnail { width: 100%; height: 200px; margin-bottom: 16px; }
        .post-content { padding-right: 0; }
    }
</style>

<div class="daangn-container">
    <header class="daangn-header">
        <a href="/" class="daangn-logo">MisteryKid Team</a>
        <nav class="daangn-nav">
            <a href="/about">팀 소개</a>
            <a href="/culture">문화</a>
            <a href="https://github.com/misterykid" target="_blank">GitHub</a>
        </nav>
    </header>

    <div style="margin-bottom: 60px;">
        <h1 style="font-size: 32px; font-weight: 800; margin-bottom: 10px;">우리가 기술로 일하는 방식</h1>
        <p style="font-size: 18px; color: #495057;">MisteryKid 기술 블로그입니다. <br>기술적인 고민과 해결 과정을 공유합니다.</p>
    </div>

    <div class="post-list">
        {% for post in site.posts limit:5 %}
        <div class="post-item">
            <div class="post-content">
                <a href="{{ post.url | relative_url }}" class="post-title">{{ post.title }}</a>
                <p class="post-excerpt">
                    {% if post.description %}
                        {{ post.description }}
                    {% else %}
                        {{ post.excerpt | strip_html | truncatewords: 20 }}
                    {% endif %}
                </p>
                <div class="post-meta">
                    <span>{{ post.author | default: "MisteryKid" }}</span> · 
                    <span>{{ post.date | date: "%Y년 %m월 %d일" }}</span>
                </div>
            </div>
            
            {% if post.image %}
            <div class="post-thumbnail">
                <a href="{{ post.url | relative_url }}">
                    <img src="{{ post.image }}" alt="Thumbnail">
                </a>
            </div>
            {% endif %}
        </div>
        {% endfor %}
    </div>

    <div style="text-align: center; margin-top: 40px; margin-bottom: 100px;">
        <a href="/archives" style="padding: 12px 30px; background: #f1f3f5; color: #495057; text-decoration: none; border-radius: 25px; font-weight: 600; font-size: 14px;">글 더보기</a>
    </div>

</div>