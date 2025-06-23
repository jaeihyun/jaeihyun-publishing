# 커스텀 도메인 설정 가이드

jaeihyun.org 도메인을 GitHub Pages에 연결하는 방법을 안내합니다.

## 🎯 설정 목표

- **현재**: https://jaeihyun.github.io/jaeihyun-publishing
- **변경 후**: https://jaeihyun.org

## 📋 사전 준비

### 1단계: 도메인 구매
- **추천 업체**: 
  - [가비아](https://www.gabia.com)
  - [후이즈](https://www.whois.co.kr)
  - [Cloudflare](https://www.cloudflare.com) (해외)
  - [Namecheap](https://www.namecheap.com) (해외)

### 2단계: DNS 설정
도메인 업체의 DNS 관리 페이지에서 다음 레코드들을 추가:

```dns
# A 레코드 (GitHub Pages IP 주소들)
Type: A
Name: @ (또는 비워둠)
Value: 185.199.108.153

Type: A  
Name: @ (또는 비워둠)
Value: 185.199.109.153

Type: A
Name: @ (또는 비워둠) 
Value: 185.199.110.153

Type: A
Name: @ (또는 비워둠)
Value: 185.199.111.153

# CNAME 레코드 (www 서브도메인)
Type: CNAME
Name: www
Value: jaeihyun.github.io
```

## 🔧 GitHub 설정

### 1단계: CNAME 파일 생성
리포지토리 루트에 `CNAME` 파일 생성:

```
jaeihyun.org
```

### 2단계: GitHub Pages 설정
1. GitHub 리포지토리 → Settings → Pages
2. Source: "Deploy from a branch" 또는 "GitHub Actions" 선택
3. Custom domain: `jaeihyun.org` 입력
4. "Enforce HTTPS" 체크 (DNS 전파 후)

## 📝 설정 파일 수정

### _quarto.yml 업데이트
```yaml
website:
  title: "jaeihyun publishing"
  site-url: "https://jaeihyun.org"  # 변경
  repo-url: "https://github.com/jaeihyun/jaeihyun-publishing"
```

### 각 책의 _quarto.yml 업데이트
```yaml
book:
  author: 
    - name: "jaeihyun"
      url: "https://jaeihyun.org"  # 변경
```

### 블로그 _quarto.yml 업데이트
```yaml
website:
  site-url: "https://jaeihyun.org/blog"  # 변경
```

## ⏱️ DNS 전파 대기

DNS 설정이 전 세계에 전파되기까지 **24-48시간** 소요될 수 있습니다.

### 전파 확인 방법
```bash
# 터미널에서 확인
nslookup jaeihyun.org

# 또는 온라인 도구 사용
# https://www.whatsmydns.net/
```

## 🔒 SSL/HTTPS 설정

### 자동 SSL (GitHub 제공)
- DNS 전파 완료 후 GitHub에서 자동으로 SSL 인증서 발급
- "Enforce HTTPS" 옵션이 활성화되면 체크

### Cloudflare 사용 (선택사항)
더 빠른 SSL과 CDN을 원한다면:

1. [Cloudflare](https://www.cloudflare.com)에 계정 생성
2. 도메인 추가 및 네임서버 변경
3. DNS 설정을 Cloudflare에서 관리
4. SSL/TLS 설정을 "Full" 또는 "Full (strict)"로 변경

## 🧪 테스트 체크리스트

### DNS 테스트
- [ ] `ping jaeihyun.org` 응답 확인
- [ ] `ping www.jaeihyun.org` 응답 확인
- [ ] 브라우저에서 접속 테스트

### 웹사이트 테스트
- [ ] 메인 페이지 정상 로드
- [ ] 도서관 페이지 접속
- [ ] 각 책 페이지 접속
- [ ] 블로그 페이지 접속
- [ ] 모바일에서 접속 테스트

### HTTPS 테스트
- [ ] https://jaeihyun.org 접속
- [ ] SSL 인증서 유효성 확인
- [ ] Mixed content 오류 없음

## 🔄 설정 완료 후 할 일

### 1단계: 모든 링크 업데이트
```bash
# 프로젝트 전체에서 이전 URL 찾아서 변경
find . -name "*.qmd" -type f -exec grep -l "jaeihyun.github.io" {} \;
```

### 2단계: 소셜 메타 태그 추가
각 페이지에 Open Graph 태그 추가:

```yaml
---
title: "페이지 제목"
description: "페이지 설명"
image: "https://jaeihyun.org/images/og-image.jpg"
---
```

### 3단계: sitemap.xml 확인
Quarto가 자동 생성하는 sitemap.xml이 새 도메인으로 업데이트되는지 확인

### 4단계: 검색엔진 등록
- [Google Search Console](https://search.google.com/search-console)
- [네이버 웹마스터도구](https://searchadvisor.naver.com)
- [Bing Webmaster Tools](https://www.bing.com/webmasters)

## 🚨 주의사항

### 이전 URL 리다이렉션
GitHub Pages는 자동으로 이전 URL을 새 도메인으로 리다이렉션하지 않습니다. 필요시 JavaScript 리다이렉션 추가:

```html
<!-- docs/404.html에 추가 -->
<script>
if (window.location.hostname === 'jaeihyun.github.io') {
  window.location.replace('https://jaeihyun.org' + window.location.pathname);
}
</script>
```

### 빌드 설정 확인
`.github/workflows/quarto-publish.yml`에 CNAME 파일 보존 설정:

```yaml
- name: Create CNAME file
  run: echo "jaeihyun.org" > docs/CNAME
  
- name: Upload artifact
  uses: actions/upload-pages-artifact@v2
  with:
    path: 'docs'
```

## 📞 문제 해결

### 일반적인 문제들

**DNS가 반영되지 않음**
- 24-48시간 대기
- 브라우저 캐시 삭제
- DNS 캐시 플러시: `ipconfig /flushdns` (Windows) 또는 `sudo dscacheutil -flushcache` (Mac)

**SSL 인증서가 발급되지 않음**
- DNS 전파 완료 확인
- GitHub Pages 설정에서 도메인 재입력
- "Enforce HTTPS" 체크박스 해제 후 재체크

**404 오류 발생**
- CNAME 파일 내용 확인
- GitHub Actions 빌드 로그 확인
- `docs/` 디렉토리에 파일들이 정상적으로 생성되었는지 확인

**일부 리소스가 로드되지 않음**
- 절대 경로를 상대 경로로 변경
- Mixed content (HTTP/HTTPS) 오류 확인

## 📊 성능 최적화

### 이미지 최적화
```bash
# 이미지 파일 압축 (예시)
# WebP 형식 사용 권장
convert image.jpg -quality 80 image.webp
```

### CDN 설정 (Cloudflare 사용시)
- 브라우저 캐시 TTL 설정
- Minification 옵션 활성화
- Brotli 압축 활성화

## 📈 분석 도구 설정

### Google Analytics
```html
<!-- _quarto.yml에 추가 -->
format:
  html:
    include-in-header: |
      <!-- Google Analytics -->
      <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
      <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());
        gtag('config', 'GA_MEASUREMENT_ID');
      </script>
```

## ✅ 최종 체크리스트

### 도메인 설정 완료
- [ ] DNS A 레코드 설정 완료
- [ ] DNS CNAME 레코드 설정 완료
- [ ] CNAME 파일 생성 완료
- [ ] GitHub Pages 설정 완료

### 파일 업데이트 완료
- [ ] _quarto.yml 사이트 URL 변경
- [ ] 각 책의 설정 파일 URL 변경
- [ ] 블로그 설정 파일 URL 변경
- [ ] README.md 링크 업데이트

### 테스트 완료
- [ ] 도메인 접속 테스트
- [ ] HTTPS 인증서 확인
- [ ] 모든 페이지 접속 테스트
- [ ] 모바일 반응형 테스트

### 추가 설정 완료
- [ ] 검색엔진 등록
- [ ] Google Analytics 설정
- [ ] 소셜 미디어 메타 태그 추가
- [ ] 성능 최적화 적용

---

🎉 **축하합니다!** jaeihyun.org 도메인 설정이 완료되었습니다!

📧 문제가 발생하면 [contact@jaeihyun.org](mailto:contact@jaeihyun.org)로 연락주세요.