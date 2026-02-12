---
layout: default
title: Home
---

<style>
    /* 1. 기본 레이아웃 설정 (사이드바 숨김 등) */
    .book-summary { display: none !important; }
    .book-body { left: 0 !important; width: 100% !important; }
    .book-header { display: none !important; }

    .blog-container {
        max-width: 800px; /* 텍스트 읽기 편한 너비 */
        margin: 0 auto;
        padding: 40px 20px;
        font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
    }

    /* 2. 헤더 영역 */
    .blog-header {
        text-align: center;
        margin-bottom: 50px;
    }


/* 프로필 이미지 */
    .profile-img {
        width: 120px;
        height: 120px;
        border-radius: 50%; /* 동그랗게 */
        object-fit: cover;
        margin-bottom: 20px;
        border: 1px solid #eaecef;
        box-shadow: 0 4px 10px rgba(0,0,0,0.05);
    }

    .blog-title {
        font-size: 32px;
        font-weight: 800;
        color: #212529;
        margin-bottom: 10px;
        letter-spacing: -0.5px;
    }
    .blog-description {
        color: #868e96;
        font-size: 18px;
    }


    /* 소셜 링크 아이콘 컨테이너 */
    .social-links {
        display: flex;
        justify-content: center;
        gap: 16px;
        margin-bottom: 40px;
    }
    
    .social-btn {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-color: #f1f3f5;
        color: #495057;
        text-decoration: none;
        transition: all 0.2s ease;
    }
    .social-btn:hover {
        background-color: #212529;
        color: white;
        transform: translateY(-3px);
    }
    .social-btn svg {
        width: 20px;
        height: 20px;
        fill: currentColor;
    }

    /* 자세히 보기(About) 버튼 */
    .about-link {
        font-size: 14px;
        color: #868e96;
        text-decoration: underline;
        cursor: pointer;
    }
    .about-link:hover { color: #212529; }

    /* 3. 카테고리 필터 버튼 (핵심 기능!) */
    .category-nav {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 10px;
        margin-bottom: 60px;
        padding-bottom: 20px;
        border-bottom: 1px solid #eaecef;
    }
    .cat-btn {
        background: white;
        border: 1px solid #dee2e6;
        padding: 8px 16px;
        border-radius: 20px;
        cursor: pointer;
        font-size: 14px;
        color: #495057;
        font-weight: 500;
        transition: all 0.2s ease;
    }
    .cat-btn:hover {
        background: #f8f9fa;
        border-color: #adb5bd;
    }
    /* 선택된 버튼 스타일 */
    .cat-btn.active {
        background: #212529; /* 검은색 배경 */
        color: white;
        border-color: #212529;
    }

    /* 4. 게시글 리스트 스타일 (카드 X, 텍스트 O) */
    .post-item {
        padding: 30px 0;
        border-bottom: 1px solid #f1f3f5;
        display: block; /* 처음에 다 보여줌 */
        transition: opacity 0.3s ease;
    }
    .post-item.hidden {
        display: none; /* 필터링되면 숨김 */
    }

    .post-meta {
        font-size: 14px;
        color: #868e96;
        margin-bottom: 8px;
        display: flex;
        align-items: center;
        gap: 10px;
    }
    .post-category-tag {
        color: #ff6b6b; /* 포인트 컬러 */
        font-weight: 600;
        font-size: 13px;
        text-transform: uppercase;
    }
    
    .post-title {
        font-size: 24px;
        font-weight: 700;
        color: #212529;
        text-decoration: none;
        margin-bottom: 12px;
        display: block;
        line-height: 1.3;
    }
    .post-title:hover {
        color: #339af0; /* 호버 시 파란색 */
    }
    
    .post-excerpt {
        font-size: 16px;
        color: #495057;
        line-height: 1.6;
        margin: 0;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }

</style>

<div class="blog-container">

    <header class="blog-header">
        <h1 class="blog-title">MisteryKid Blog</h1>
        <p class="blog-description">공부하고 기록하는 공간</p>
    </header>

    <nav class="category-nav" id="categoryNav">
        <button class="cat-btn active" onclick="filterPosts('all', this)">All</button>
        
        {% for category in site.categories %}
            <button class="cat-btn" onclick="filterPosts('{{ category | first }}', this)">
                {{ category | first | upcase }}
            </button>
        {% endfor %}
    </nav>

    <div class="post-list">
        {% for post in site.posts %}
        <article class="post-item" data-category="{{ post.categories | first }}">
            
            <div class="post-meta">
                <span class="post-category-tag">{{ post.categories | first | upcase }}</span>
                <span>·</span>
                <span>{{ post.date | date: "%Y.%m.%d" }}</span>
            </div>

            <a href="{{ post.url | relative_url }}" class="post-title">
                {{ post.title }}
            </a>

            <p class="post-excerpt">
                {% if post.description %}
                    {{ post.description }}
                {% else %}
                    {{ post.excerpt | strip_html | truncatewords: 30 }}
                {% endif %}
            </p>
        </article>
        {% endfor %}
    </div>

</div>

<script>
    function filterPosts(category, btnElement) {
        // 1. 모든 게시글 가져오기
        var posts = document.getElementsByClassName('post-item');
        
        // 2. 버튼 스타일 변경 (Active 옮기기)
        var buttons = document.getElementsByClassName('cat-btn');
        for (var i = 0; i < buttons.length; i++) {
            buttons[i].classList.remove('active');
        }
        btnElement.classList.add('active');

        // 3. 실제 필터링 로직
        for (var i = 0; i < posts.length; i++) {
            var postCat = posts[i].getAttribute('data-category');
            
            if (category === 'all') {
                // 'All'이면 전부 보여주기
                posts[i].classList.remove('hidden');
            } else {
                // 선택한 카테고리와 같으면 보여주고, 아니면 숨기기
                if (postCat === category) {
                    posts[i].classList.remove('hidden');
                } else {
                    posts[i].classList.add('hidden');
                }
            }
        }
    }
</script>