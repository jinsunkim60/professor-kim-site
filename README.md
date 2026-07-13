# 김진선 홈페이지 (Astro)

정적 사이트 이전 프로젝트 — Phase 1 (사이트 뼈대 + 홈 + 4축 + 자료실 + Q&A 자리 + 소개).

## 빠른 시작

Node.js 18.14 이상이 필요합니다.

```bash
npm install      # 의존성 설치
npm run dev      # 개발 서버 (http://localhost:4321)
npm run build    # 정적 빌드 → dist/ 폴더 생성
npm run preview  # 빌드 결과 미리보기
```

> 참고: 이 프로젝트는 Anthropic 작업 환경(네트워크 제한)에서 `npm install`을 실행하지 못해 **빌드 검증은 교수님 PC 또는 배포 CI에서** 이뤄집니다. 표준 Astro 5 구성이라 그대로 빌드됩니다. 혹시 오류가 나면 메시지를 그대로 보내주세요 — 바로 잡아드립니다.

## 폴더 구조

```
src/
  layouts/Base.astro        공통 레이아웃 (헤더·푸터·다크모드)
  components/Nav.astro       상단 네비게이션
  components/Footer.astro    푸터
  styles/global.css          디자인 시스템 (색·서체·컴포넌트)
  data/axes.js               4개 축 정의 (라벨·색·설명)
  content/config.ts          콘텐츠 스키마 (글·자료)
  content/posts/*.md         글 (가르치다·설계하다·만들다·쓰다)
  content/materials/*.md     강의자료 항목
  pages/index.astro          홈
  pages/[axis].astro         축별 목록 (/teach /design /build /write)
  pages/posts/[...id].astro  글 상세
  pages/materials.astro      자료실
  pages/qna.astro            Q&A (Phase 3.5에서 게시판 연동)
  pages/about.astro          소개
public/files/                다운로드용 강의자료 파일 (PDF·ZIP)
```

## 글 추가하기

`src/content/posts/` 에 `.md` 파일을 만들면 홈·축 목록·상세 페이지에 자동 반영됩니다.

```markdown
---
title: 글 제목
date: 2026-07-13
axis: teach        # teach | design | build | write 중 하나
summary: 한 줄 요약
featured: false    # 대표 에세이로 홈에 크게 띄우려면 true
---

여기에 본문을 Markdown으로 작성합니다.
```

## 강의자료 추가하기

1. 파일(PDF·ZIP 등)을 `public/files/` 에 넣습니다. 예: `public/files/lecture01.pdf`
2. `src/content/materials/` 에 `.md` 파일을 만듭니다.

```markdown
---
title: 1주차 · 개요 강의 슬라이드
date: 2026-07-13
course: 회로이론
summary: 강의 개요 (PDF)
file: /files/lecture01.pdf
---
```

## 배포 (권장: Cloudflare Pages — 무료)

1. 이 폴더를 GitHub 저장소에 올립니다.
2. Cloudflare Pages(또는 Netlify)에서 저장소를 연결합니다.
3. 빌드 설정: **빌드 명령** `npm run build`, **출력 디렉터리** `dist`.
4. 도메인 `blog.professor-kim.com` 을 연결합니다. (현재 WordPress에서 옮겨오는 형태)
   - `astro.config.mjs` 의 `site` 값을 실제 도메인으로 유지/수정하세요.

배포 CI가 `npm install` 과 `npm run build` 를 자동으로 실행하므로, 교수님이 직접 빌드하지 않아도 됩니다.

## 다음 단계 (로드맵)

- **Phase 2** — 기존 WordPress 글·소개 이전.
- **Phase 3** — 각 축 콘텐츠 채우기, 실제 강의자료 업로드, YouTube·GitHub 연결.
- **Phase 3.5** — Q&A 게시판(Supabase + 구글·이메일 로그인) 구현. `pages/qna.astro` 를 실제 게시판으로 교체.
- **Phase 4** — SEO·RSS·구독·통계, 발행 루틴.

## 디자인 메모

- 색·서체는 `src/styles/global.css` 상단의 CSS 변수에서 한 번에 조정합니다.
- 라이트/다크는 우측 상단 ◐ 버튼으로 전환되며 브라우저에 기억됩니다.
- 4축 색: 가르치다(청록) · 설계하다(파랑) · 만들다(주황) · 쓰다(로즈).
