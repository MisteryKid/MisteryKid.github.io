---
layout: default
title: Home
---

<style>
    /* 기본 레이아웃 리셋 */
    .book-summary, .book-header { display: none !important; }
    .book-body { left: 0 !important; width: 100% !important; padding: 0 !important; }

    .blog-container {
        max-width: 800px;
        margin: 0 auto;
        padding: 60px 20px;
        font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
    }

    /* 1. 프로필 헤더 영역 */
    .blog-header { text-align: center; margin-bottom: 50px; }
    
    .profile-img {
        width: 120px; height: 120px;
        border-radius: 50%;
        object-fit: cover;
        margin-bottom: 20px;
        border: 1px solid #eaecef;
        box-shadow: 0 8px 20px rgba(0,0,0,0.1); /* 그림자 약간 더 진하게 */
        transition: transform 0.3s ease;
    }
    .profile-img:hover { transform: scale(1.05); } /* 마우스 올리면 살짝 커짐 */

    .blog-title {
        font-size: 32px; font-weight: 800; color: #212529;
        margin-bottom: 10px; letter-spacing: -0.5px;
    }
    .blog-description { color: #495057; font-size: 17px; line-height: 1.6; max-width: 500px; margin: 0 auto 24px auto; }

    /* 소셜 아이콘 */
    .social-links { display: flex; justify-content: center; gap: 16px; margin-bottom: 40px; }
    .social-btn {
        display: flex; align-items: center; justify-content: center;
        width: 42px; height: 42px; border-radius: 50%;
        background-color: #f8f9fa; border: 1px solid #eaecef;
        color: #495057; text-decoration: none; transition: all 0.2s ease;
    }
    .social-btn:hover { background-color: #212529; color: white; border-color: #212529; transform: translateY(-3px); }
    .social-btn svg { width: 20px; height: 20px; fill: currentColor; }

    /* 2. 카테고리 필터 (Sticky 적용: 스크롤 내려도 상단에 붙음) */
    .category-nav {
        display: flex; justify-content: center; flex-wrap: wrap; gap: 8px;
        margin-bottom: 40px; padding: 15px 0;
        background: rgba(255, 255, 255, 0.95); /* 배경 살짝 불투명 */
        position: sticky; top: 0; z-index: 100; /* 스크롤 시 상단 고정 */
        border-bottom: 1px solid #f1f3f5;
        backdrop-filter: blur(5px);
    }
    .cat-btn {
        background: white; border: 1px solid #dee2e6;
        padding: 6px 14px; border-radius: 20px;
        cursor: pointer; font-size: 14px; color: #495057; font-weight: 600;
        transition: all 0.2s ease;
    }
    .cat-btn:hover { background: #f1f3f5; }
    .cat-btn.active { background: #212529; color: white; border-color: #212529; }

    /* 3. 게시글 리스트 */
    .post-list { min-height: 300px; } /* 필터링 시 높이 흔들림 방지 */
    
    .post-item {
        padding: 30px 0; border-bottom: 1px solid #f1f3f5;
        display: block;
        opacity: 1; transform: translateY(0);
        transition: opacity 0.3s ease, transform 0.3s ease; /* 부드러운 애니메이션 */
    }
    
    /* 숨김 처리 스타일 (애니메이션용) */
    .post-item.hidden {
        display: none; 
        opacity: 0; 
        transform: translateY(20px);
    }

    .post-meta { font-size: 14px; color: #868e96; margin-bottom: 8px; display: flex; align-items: center; gap: 8px; }
    .post-category-tag { color: #ff6b6b; font-weight: 700; font-size: 12px; text-transform: uppercase; background: #fff5f5; padding: 2px 6px; border-radius: 4px; }
    
    .post-title { font-size: 22px; font-weight: 700; color: #212529; text-decoration: none; margin-bottom: 10px; display: block; line-height: 1.35; transition: color 0.2s; }
    .post-title:hover { color: #339af0; }
    
    .post-excerpt { font-size: 16px; color: #495057; line-height: 1.6; margin: 0; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }

    /* 모바일 대응 */
    @media (max-width: 500px) {
        .blog-title { font-size: 26px; }
        .post-title { font-size: 20px; }
        .profile-img { width: 100px; height: 100px; }
    }
</style>

<div class="blog-container">

    <header class="blog-header">
        
        <h1 class="blog-title">MisteryKid's TECH-BLOG</h1>
        <p class="blog-description">
            ROS2 · Linux · <br>
            공부하고 기록하는 공간.
        </p>

        <div class="social-links">
            <a href="https://github.com/misterykid" target="_blank" class="social-btn" title="GitHub">
                <svg viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
            </a>
            <a href="mailto:your_email@gmail.com" class="social-btn" title="Email">
                <svg viewBox="0 0 24 24"><path d="M0 3v18h24v-18h-24zm21.518 2l-9.518 7.713-9.518-7.713h19.036zm-19.518 14v-11.817l10 8.104 10-8.104v11.817h-20z"/></svg>
            </a>
            <a href="/about/" class="social-btn" title="About">
                <svg viewBox="0 0 24 24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/></svg>
            </a>
            <a href="/search/" class="social-btn" title="Search">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="11" cy="11" r="8"></circle>
                    <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                </svg>
            </a>



        </div>
    </header>

    <nav class="category-nav" id="categoryNav">
        <button class="cat-btn active" onclick="filterPosts('all', this)">ALL</button>
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
                <span>{{ post.date | date: "%Y.%m.%d" }}</span>
            </div>
            <a href="{{ post.url | relative_url }}" class="post-title">
                {{ post.title }}
            </a>
            <p class="post-excerpt">
                {% if post.description %}
                    {{ post.description }}
                {% else %}
                    {{ post.excerpt | strip_html | truncatewords: 25 }}
                {% endif %}
            </p>
        </article>
        {% endfor %}
    </div>

</div>

<script>
    function filterPosts(category, btnElement) {
        var posts = document.getElementsByClassName('post-item');
        
        // 버튼 활성화 스타일 변경
        var buttons = document.getElementsByClassName('cat-btn');
        for (var i = 0; i < buttons.length; i++) {
            buttons[i].classList.remove('active');
        }
        btnElement.classList.add('active');

        // 필터링 로직
        for (var i = 0; i < posts.length; i++) {
            var postCat = posts[i].getAttribute('data-category');
            var el = posts[i];
            
            if (category === 'all' || postCat === category) {
                // 보여주기
                el.classList.remove('hidden');
                // 약간의 딜레이 후 투명도 복구 (애니메이션용)
                setTimeout((function(e) { return function() { e.style.opacity = '1'; e.style.transform = 'translateY(0)'; }; })(el), 50);
            } else {
                // 숨기기
                el.style.opacity = '0';
                el.style.transform = 'translateY(20px)';
                el.classList.add('hidden');
            }
        }
    }
</script>