---
layout: default
title: Search
permalink: /search/
---

<style>
    /* 검색 페이지 전용 스타일 */
    .search-container {
        max-width: 680px;
        margin: 60px auto;
        padding: 0 20px;
        font-family: -apple-system, BlinkMacSystemFont, "Pretendard", sans-serif;
    }

    .search-box {
        position: relative;
        width: 100%;
        margin-bottom: 50px;
    }

    /* 검색 입력창 */
    #search-input {
        width: 100%;
        padding: 20px 20px 20px 50px; /* 아이콘 공간 확보 */
        font-size: 18px;
        border: 2px solid #eaecef;
        border-radius: 12px;
        background-color: #f8f9fa;
        transition: all 0.2s ease;
        box-sizing: border-box;
        outline: none;
    }
    #search-input:focus {
        border-color: #212529;
        background-color: #fff;
        box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    }

    /* 돋보기 아이콘 */
    .search-icon {
        position: absolute;
        top: 50%;
        left: 20px;
        transform: translateY(-50%);
        color: #adb5bd;
        pointer-events: none;
    }

    /* 검색 결과 리스트 */
    #results-container {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .search-result-item {
        padding: 24px 0;
        border-bottom: 1px solid #f1f3f5;
        animation: fadeIn 0.3s ease;
    }
    .search-result-item a {
        text-decoration: none;
        display: block;
    }
    
    .result-title {
        font-size: 20px;
        font-weight: 700;
        color: #212529;
        margin-bottom: 8px;
        line-height: 1.4;
    }
    .result-title:hover { color: #339af0; }

    .result-meta {
        font-size: 13px;
        color: #868e96;
        text-transform: uppercase;
        font-weight: 600;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(10px); }
        to { opacity: 1; transform: translateY(0); }
    }
</style>

<div class="search-container">
    
    <div class="search-box">
        <svg class="search-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
        
        <input type="text" id="search-input" placeholder="검색어를 입력하세요 (예: ROS2, Memory...)">
    </div>

    <ul id="results-container"></ul>

</div>

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>

<script>
    var sjs = SimpleJekyllSearch({
        searchInput: document.getElementById('search-input'),
        resultsContainer: document.getElementById('results-container'),
        
        // ▼▼▼ [중요] 여기를 수정하세요! ▼▼▼
        // 기존: json: '/search.json',
        json: '{{ "/search.json" | relative_url }}', 
        // ▲▲▲ 이렇게 바꾸면 깃허브에서도 정확한 경로를 찾습니다.
        
        searchResultTemplate: `
            <li class="search-result-item">
                <a href="{url}">
                    <div class="result-title">{title}</div>
                    <div class="result-meta">{category} · {date}</div>
                </a>
            </li>
        `,
        noResultsText: '<li style="color:#868e96; text-align:center; padding:20px;">검색 결과가 없습니다.</li>',
        limit: 10,
        fuzzy: false
    });
</script>