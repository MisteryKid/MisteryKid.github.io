---
layout: default
title: Home
---

<style>
    /* 1. 기본 레이아웃 리셋 */
    .book-summary { display: none !important; }
    .book-body { left: 0 !important; width: 100% !important; padding: 0 !important; }
    .book-header { display: none !important; }

    .blog-container {
        max-width: 800px;
        margin: 0 auto;
        padding: 60px 20px;
        font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
    }

    /* 2. 헤더 영역 (텍스트 중심) */
    .blog-header {
        text-align: center;
        margin-bottom: 60px; /* 여백 넉넉하게 */
    }
    .blog-title {
        font-size: 42px; /* 제목을 더 크고 임팩트 있게 */
        font-weight: 900;
        color: #212529;
        margin-bottom: 16px;
        letter-spacing: -1px;
    }
    .blog-description {
        color: #868e96;
        font-size: 20px;
        font-weight: 400;
        line-height: 1.5;
    }

    /* 3. 카테고리 필터 버튼 */
    .category-nav {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 10px;
        margin-bottom: 50px;
        padding-bottom: 20px;
        border-bottom: 1px solid #eaecef;
    }
    .cat-btn {
        background: white;
        border: 1px solid #dee2e6;
        padding: 8px 18px;
        border-radius: 24px;
        cursor: pointer;
        font-size: 15px;
        color: #495057;
        font-weight: 600;
        transition: all 0.2s ease;
    }
    .cat-btn:hover {
        background: #f8f9fa;
        border-color: #adb5bd;
    }
    .cat-btn.active {
        background: #212529;
        color: white;
        border-color: #212529;
    }

    /* 4. 게시글 리스트 스타일 */
    .post-item {
        padding: 36px 0;
        border-bottom: 1px solid #f1f3f5;
        display: block;
        transition: opacity 0.2s ease;
    }
    .post-item:last-child { border-bottom: none; } /* 마지막 선 제거 */
    
    .post-item.hidden { display: none; } /* 필터링 숨김 */

    .post-meta {
        font-size: 14px;
        color: #868e96;
        margin-bottom: 10px;
        display: flex;
        align-items: center;
        gap: 8px;
    }
    .post-category-tag {
        color: #fa5252; /* 붉은 계열 포인트 */
        font-weight: 700;
        font-size: 13px;
        text-transform: uppercase;
    }
    
    .post-title {
        font-size: 26px;
        font-weight: 800;
        color: #212529;
        text-decoration: none;
        margin-bottom: 14px;
        display: block;
        line-height: 1.3;
        transition: color 0.2s;
    }
    .post-title:hover {
        color: #228be6; /* 호버 시 파란색 포인트 */
    }
    
    .post-excerpt {
        font-size: 16px;
        color: #495057;
        line-height: 1.65;
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
        var posts = document.getElementsByClassName('post-item');
        
        // 버튼 활성화
        var buttons = document.getElementsByClassName('cat-btn');
        for (var i = 0; i < buttons.length; i++) {
            buttons[i].classList.remove('active');
        }
        btnElement.classList.add('active');

        // 필터링
        for (var i = 0; i < posts.length; i++) {
            var postCat = posts[i].getAttribute('data-category');
            
            if (category === 'all') {
                posts[i].classList.remove('hidden');
            } else {
                if (postCat === category) {
                    posts[i].classList.remove('hidden');
                } else {
                    posts[i].classList.add('hidden');
                }
            }
        }
    }
</script>