# 📁 Jekyll 블로그 카테고리 & 하위 카테고리 관리 가이드

이 문서는 블로그에 새로운 **상위 카테고리** 및 **하위 카테고리**를 추가하고 관리하는 방법을 설명하는 가이드라인입니다. 현재 블로그는 홈 화면(`index.md`)의 2단계 필터링 버튼과 좌측 사이드바(`toc-date.html`) 목차가 유기적으로 연동되어 있습니다.

---

## 1. 카테고리 구조 요약

게시글 마크다운(`.md`) 파일 상단 머리말(Frontmatter)의 `categories` 배열을 기준으로 작동합니다.

* **상위 카테고리**: 배열의 **첫 번째** 값 (예: `Study`, `Daily`, `Robotics`)
* **하위 카테고리**: 배열의 **두 번째** 값 (예: `Design Pattern`, `DDS_TEST`)

---

## 2. 새 글 작성 및 카테고리 적용 가이드

### 💡 Case A. 상위 카테고리만 지정할 경우 (일반 게시글)
하위 구분 없이 상위 카테고리에만 속하는 글을 작성할 때의 설정입니다.

1. `_posts/Study/` 또는 `_posts/Daily/` 등의 폴더에 마크다운 파일을 생성합니다.
2. 머리말(Frontmatter)을 아래와 같이 작성합니다:
   ```yaml
   ---
   title: 나의 일반 연구 기록
   author: Chaewon Kim
   date: 2026-07-03
   categories: [Study]       # 첫 번째 인자만 설정 (또는 category: Study)
   layout: post
   ---
   ```

---

### 💡 Case B. 하위 카테고리(폴더)를 추가하고 싶을 경우
예를 들어 **Study** 하위에 **System** 카테고리를 새로 추가하고 싶을 때의 과정입니다.

1. **물리적 폴더 생성 (권장)**
   * `_posts/Study/System/` 또는 `_posts/Study/TODO/` 폴더를 생성합니다. (경로는 필수가 아니나, 관리 편의성을 위해 폴더 구분을 권장합니다.)

2. **포스트 파일 작성 및 `categories` 지정**
   * 해당 폴더에 포스트 파일(예: `2026-07-03-Memory.md`)을 작성하고 머리말을 설정합니다:
     ```yaml
     ---
     title: 메모리 아키텍처 공부
     author: Chaewon Kim
     date: 2026-07-03
     categories: [Study, System]  # [상위, 하위] 순으로 적어주세요.
     layout: post
     ---
     ```
     > [!IMPORTANT]
     > 하위 카테고리명(`System`, `TODO`, `Design Pattern`)은 버튼과 사이드바에 표시될 이름이므로, 띄어쓰기와 대소문자를 예쁘게 맞춰 작성하시는 것이 좋습니다.

3. **자동 반영 확인**
   * Jekyll이 빌드되면서 아래 내용이 자동으로 업데이트됩니다:
     * **홈 화면(`index.md`)**: `STUDY` 버튼을 누르면 하단에 `System (5)` 또는 `TODO (1)` 하위 카테고리 필터 버튼이 자동으로 나타납니다.
     * **좌측 사이드바**: `📁 STUDY` 트리 하위에 `📂 System`, `📂 TODO` 폴더 그룹이 생기고 그 밑에 글이 들어갑니다.
     * **포스트 본문 상단**: 카테고리가 `STUDY / SYSTEM` 형태로 노출됩니다.

---

## 3. 권장 디렉토리 구조 예시

블로그 포스트 파일들을 깔끔하게 관리하기 위한 추천 폴더 구조입니다.

```text
MisteryKid.github.io/
├── _posts/
│   ├── Daily/
│   │   ├── Setting/
│   │   │   └── 2026-02-27-tmux.md        # categories: [Daily, Setting]
│   │   ├── Life/
│   │   │   └── 2025-12-24-English.md     # categories: [Daily, Life]
│   │   └── Thoughts/
│   │       └── 2026-02-27-Prompt.md      # categories: [Daily, Thoughts]
│   ├── Experiment/
│   │   ├── ROS2/
│   │   │   └── 2026-01-02-DDSexp.md      # categories: [Experiment, ROS2]
│   │   ├── Dataset/
│   │   │   └── 2026-05-18-nuScenes.md    # categories: [Experiment, Dataset]
│   │   └── Utility/
│   │       └── 2026-02-13-analisis.md    # categories: [Experiment, Utility]
│   └── Study/
│       ├── TODO/
│       │   └── 2026-02-13-whattostudy.md # categories: [Study, TODO]
│       ├── ROS2/
│       │   └── 2026-01-21-Priority.md    # categories: [Study, ROS2]
│       ├── System/
│       │   ├── 2026-01-27-cgroup.md      # categories: [Study, System]
│       │   └── 2026-02-12-Memory.md      # categories: [Study, System]
│       └── Design_Pattern/
│           ├── 2026-04-11-SOLID.md       # categories: [Study, Design Pattern]
│           └── 2026-06-01-WhatIs.md      # categories: [Study, Design Pattern]
```

---

## 4. 문제 해결 및 팁 (Troubleshooting)

* **Q. 하위 카테고리가 홈 화면 상단(ALL 옆)에 독립된 큰 버튼으로 떠요!**
  * **원인**: 포스트 머리말에 `categories: [Design Pattern]`과 같이 하위 카테고리만 단독으로 적었기 때문입니다.
  * **해결**: 반드시 `categories: [Study, Design Pattern]`처럼 상위 카테고리를 첫 번째 요소로 함께 명시해 주어야 정상적인 2단 구조로 분류됩니다.
* Q. 카테고리 이름을 수정하고 싶어요.
  * 해당 하위 카테고리에 속한 모든 마크다운 파일들의 `categories: [...]` 설정 내 텍스트를 일괄 수정해 주시면 빌드 시 자동 변경됩니다.

---

## 5. 📷 이미지 자산 관리 가이드

블로그에 이미지를 쉽고 일관성 있게 추가하기 위해 VS Code 자동 복사 설정을 완료했습니다.

### ⚙️ VS Code 이미지 자동 설정 내역
프로젝트 루트의 `.vscode/settings.json`에 규칙을 추가하여, 포스트 마크다운 파일에 이미지를 복사-붙여넣기(Ctrl+V)하면 **해당 포스트의 카테고리 폴더로 이미지 파일이 자동으로 복사**되고 절대 경로로 링크가 삽입됩니다.

* **동작 매핑 예시**:
  * `_posts/Study/ROS2/`의 글에 붙여넣기 ➔ `/assets/img/posts/Study/ROS2/` 폴더로 이미지 자동 이동 및 `/assets/img/posts/Study/ROS2/image.png` 형식의 링크 삽입
  * `_posts/Daily/Setting/`의 글에 붙여넣기 ➔ `/assets/img/posts/Daily/Setting/` 폴더로 이미지 자동 이동 및 `/assets/img/posts/Daily/Setting/image.png` 형식의 링크 삽입
  * `_posts/Experiment/ROS2/`의 글에 붙여넣기 ➔ `/assets/img/posts/Experiment/ROS2/` 폴더로 이미지 자동 이동 및 `/assets/img/posts/Experiment/ROS2/image.png` 형식의 링크 삽입

### 📝 수동 작성 시 이미지 경로
마크다운에 이미지를 직접 작성할 때는 항상 **블로그 root 기준 절대 경로(슬래시 `/`로 시작)**로 작성해 주세요.
```markdown
![설명](/assets/img/posts/Study/ROS2/image_name.png)
```
> [!NOTE]
> 상대 경로(`../../../assets/...`)로 작성하면 글이 하위 폴더로 이동할 때 경로가 깨지기 쉽지만, 루트 기준 절대 경로(`/assets/...`)로 작성하면 언제 어디서든 경로가 항상 유지되므로 훨씬 안전합니다.
