# jaeihyun publishing

> 인문학과 일상을 담은 디지털 도서관

[![Build and Deploy](https://github.com/jaeihyun/jaeihyun-publishing/actions/workflows/quarto-publish.yml/badge.svg)](https://github.com/jaeihyun/jaeihyun-publishing/actions/workflows/quarto-publish.yml)
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

## 📖 소개

**jaeihyun publishing**은 일상의 경험을 책으로 엮어 나누는 개인 전자출판 플랫폼입니다. [Quarto](https://quarto.org)를 기반으로 구축되었으며, GitHub Pages를 통해 무료로 서비스되고 있습니다.

🌐 **웹사이트**: [https://jaeihyun.github.io/jaeihyun-publishing](https://jaeihyun.github.io/jaeihyun-publishing)

## 📚 출간 도서

### 완결 작품
- **[시골 경험기](https://jaeihyun.github.io/jaeihyun-publishing/books/rural-experience/)**: 도시를 떠나 자연과 함께한 1년의 기록

### 연재 중
- **[도시 일기](https://jaeihyun.github.io/jaeihyun-publishing/books/urban-diary/)**: 메트로폴리스에서 발견한 인간의 모습들

### 예정
- **여행 수첩**: 세계 곳곳에서 마주한 문화와 사람들

## ✨ 플랫폼 특징

- **🆓 무료 접근**: 모든 콘텐츠를 온라인에서 무료로 읽기 가능
- **📱 반응형 디자인**: PC, 태블릿, 모바일 모든 기기에서 최적화된 읽기 경험
- **🔍 통합 검색**: 전체 사이트를 아우르는 통합 검색 기능
- **🏷️ 태그 시스템**: 주제별, 카테고리별 콘텐츠 분류
- **💬 독자 소통**: GitHub Issues/Discussions를 통한 독자와의 소통
- **📖 다양한 형식**: HTML, PDF, EPUB 등 다양한 형식 지원

## 🛠️ 기술 스택

- **[Quarto](https://quarto.org)**: 과학적 출판을 위한 오픈소스 도구
- **[GitHub Pages](https://pages.github.com)**: 무료 웹 호스팅
- **[GitHub Actions](https://github.com/features/actions)**: 자동 빌드 및 배포
- **[Bootstrap](https://getbootstrap.com)**: 반응형 웹 디자인
- **[Nord Theme](https://www.nordtheme.com)**: 색상 팔레트
- **[Noto Fonts](https://fonts.google.com/noto)**: 한글 최적화 폰트

## 📁 프로젝트 구조

```
jaeihyun-publishing/
├── _quarto.yml                 # 메인 웹사이트 설정
├── index.qmd                   # 홈페이지
├── library.qmd                 # 도서관 페이지
├── about.qmd                   # 저자 소개
├── 
├── books/                      # 도서 디렉토리
│   ├── rural-experience/       # 시골 경험기
│   ├── urban-diary/           # 도시 일기
│   └── travel-notes/          # 여행 수첩
│
├── blog/                      # 블로그 시스템
│   ├── _quarto.yml           # 블로그 설정
│   ├── index.qmd             # 블로그 홈
│   └── posts/                # 포스트들
│
├── styles/                   # 스타일시트
│   ├── main.scss            # 메인 SCSS
│   └── korean.css           # 한글 최적화
│
├── images/                   # 이미지 리소스
├── docs/                     # 빌드 결과물 (자동 생성)
└── .github/workflows/        # GitHub Actions
    └── quarto-publish.yml   # 자동 배포 설정
```

## 🚀 로컬 개발

### 필요 조건
- [Quarto](https://quarto.org/docs/get-started/) 설치
- [Git](https://git-scm.com/) 설치

### 설치 및 실행
```bash
# 저장소 클론
git clone https://github.com/jaeihyun/jaeihyun-publishing.git
cd jaeihyun-publishing

# 미리보기 서버 실행
quarto preview

# 빌드
quarto render
```

### 새 책 추가하기
```bash
# books 디렉토리에 새 폴더 생성
mkdir books/new-book

# 책 설정 파일 생성
cp books/rural-experience/_quarto.yml books/new-book/
# _quarto.yml 내용 수정

# 메인 _quarto.yml의 sidebar에 새 책 추가
```

## 🎨 커스터마이징

### 색상 테마 변경
`styles/main.scss`에서 색상 변수들을 수정:

```scss
$primary: #5E81AC;    // 주 색상
$secondary: #81A1C1;  // 보조 색상
$success: #A3BE8C;    // 성공 색상
```

### 폰트 변경
`styles/korean.css`에서 폰트 설정 수정:

```css
@import url('원하는-폰트-URL');

body {
  font-family: "원하는폰트", sans-serif;
}
```

## 📝 콘텐츠 작성 가이드

### 새 책 챕터 작성
```markdown
---
title: "챕터 제목"
---

# 챕터 내용

본문 내용을 여기에 작성합니다.

::: {.chapter-intro}
*장 소개 문구*
:::

## 소제목

내용...

::: {.chapter-end}
**다음 장에서는**: 다음 내용 예고

[📖 다음 장](next-chapter.qmd){.btn .btn-primary}
:::
```

### 블로그 포스트 작성
```markdown
---
title: "포스트 제목"
author: "jaeihyun"
date: "2025-06-21"
categories: [카테고리1, 카테고리2]
tags: [태그1, 태그2]
---

포스트 내용...
```

## 🤝 기여하기

### 오타 신고
- [Issues](https://github.com/jaeihyun/jaeihyun-publishing/issues)에서 오타나 오류 신고
- Pull Request로 직접 수정 제안

### 번역
- 다국어 번역 프로젝트에 참여
- [Discussions](https://github.com/jaeihyun/jaeihyun-publishing/discussions)에서 번역 관련 논의

### 피드백
- 독서 후기나 개선 제안을 [Discussions](https://github.com/jaeihyun/jaeihyun-publishing/discussions)에 공유

## 📄 라이선스

이 프로젝트는 [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/) 하에 공개됩니다.

### 이는 다음을 의미합니다:

- ✅ **자유로운 사용**: 상업적 목적 포함 자유롭게 사용 가능
- ✅ **수정 및 배포**: 내용을 수정하고 재배포 가능
- ✅ **출처 표시 필수**: 원작자(jaeihyun) 및 원본 링크 표시 필요
- ✅ **동일 라이선스**: 수정된 작품도 같은 라이선스로 공개

## 💬 연락처

- **이메일**: [contact@jaeihyun.org](mailto:contact@jaeihyun.org)
- **GitHub**: [@jaeihyun](https://github.com/jaeihyun)
- **웹사이트**: [jaeihyun.org](https://jaeihyun.org)

## 🙏 감사의 말

이 플랫폼은 다음 오픈소스 프로젝트들의 도움으로 만들어졌습니다:

- [Quarto](https://quarto.org) - 과학적 출판 도구
- [GitHub](https://github.com) - 코드 저장소 및 호스팅
- [Bootstrap](https://getbootstrap.com) - CSS 프레임워크
- [Google Fonts](https://fonts.google.com) - 웹 폰트
- [Lucide](https://lucide.dev) - 아이콘

---

⭐ 이 프로젝트가 도움이 되었다면 Star를 눌러주세요!  
📖 새로운 콘텐츠 알림을 받으려면 Watch를 설정해주세요!