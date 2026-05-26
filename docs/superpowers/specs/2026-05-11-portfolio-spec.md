# 정재훈 포트폴리오 — 프로젝트 명세서

**문서 버전:** 1.0  
**작성일:** 2026-05-11  
**대상 파일:** `index.html` (단일 파일 정적 사이트)  
**배포 방식:** GitHub Pages 또는 정적 호스팅 (빌드 툴 없음)

---

## 1. 프로젝트 개요

정재훈(Jung Jaehun, 1998년생)의 개인 커리어 포트폴리오 사이트.
Data & Product 직군 취업을 목표로 하며, 프로젝트 경험·수상 이력·경력을 하나의 편집 인쇄물(Editorial) 스타일로 담아낸다.

### 핵심 원칙

- **OBYS® 스타일 레스트레인트**: 검정/흰색, 1px 헤어라인, 넉넉한 여백. 색은 악센트로만.
- **단일 HTML 파일**: 빌드 없이 index.html 하나로 완결. 외부 의존성은 폰트 CDN만.
- **컨텐츠 진실성**: 과대해석 없이 실제 프로젝트와 정확히 일치하는 copy.
- **가시성 우선**: 영문 헤더 + 한국어 서브텍스트로 신규 방문자도 즉시 파악 가능.

---

## 2. 디자인 토큰 (CSS Custom Properties)

### 2.1 라이트 테마 (기본)

```css
:root {
  /* 배경 */
  --bg:      #F5F3ED;   /* 따뜻한 양피지 크림 */
  --bg-elev: #FFFFFF;   /* 카드 표면 */
  --bg-soft: #ECE9E0;   /* 인셋 영역 */

  /* 텍스트 */
  --ink:     #0E0E0E;   /* 주 텍스트 */
  --ink-2:   #3A3A3A;   /* 보조 텍스트 */
  --ink-3:   #7E7C75;   /* 힌트 / 메타 */

  /* 선 */
  --line:      rgba(14,14,14,0.10);
  --line-soft: rgba(14,14,14,0.05);

  /* 액센트 */
  --orange: #FF3E00;   /* 주 액센트 (수상, 강조) */
  --blue:   #4A90A4;   /* 보조 노트 구분선 */
  --tan:    #C5A77E;   /* 예비 (현재 미사용) */

  /* 공간 */
  --r:    12px;
  --r-lg: 16px;
  --pad-x: max(20px, 5vw);
  --max-w: 1400px;

  /* 폰트 */
  --font-display: 'Inter', 'Pretendard Variable', -apple-system, sans-serif;
  --font-body:    'Pretendard Variable', 'Inter', -apple-system, sans-serif;
  --font-mono:    'JetBrains Mono', ui-monospace, monospace;

  /* 이징 */
  --ease: cubic-bezier(0.22, 1, 0.36, 1);
}
```

### 2.2 다크 테마 (JS 토글)

JS로 `document.documentElement.style.setProperty()`를 통해 개별 변수를 오버라이드.

| 변수 | 다크 값 |
|---|---|
| `--bg` | `#0E0E0E` |
| `--bg-elev` | `#181818` |
| `--bg-soft` | `#1F1F1F` |
| `--ink` | `#F5F3ED` |
| `--ink-2` | `#BFBDB6` |
| `--ink-3` | `#7E7C75` |
| `--line` | `rgba(255,255,255,0.10)` |
| `--line-soft` | `rgba(255,255,255,0.05)` |

---

## 3. 타이포그래피 스택

| 용도 | 폰트 | CDN |
|---|---|---|
| 디스플레이 / 헤딩 | Inter (400–900) | Google Fonts |
| 본문 / UI | Pretendard Variable | jsdelivr CDN |
| 코드 / 레이블 | JetBrains Mono (400–700) | Google Fonts |

타이포그래피 스케일은 `clamp()` 기반 유동형.

| 요소 | 크기 |
|---|---|
| Hero 타이틀 | `clamp(44px, 9vw, 160px)` |
| 섹션 헤더 | `clamp(32px, 4.6vw, 64px)` |
| 프로젝트 이름 | `clamp(32px, 4.6vw, 64px)` |
| 프로세스 헤딩 | `clamp(26px, 3vw, 44px)` |
| 본문 | 15–16px |
| 메타 레이블 | 11–12px, letter-spacing .1em |

---

## 4. 정보 구조 (IA) — 9개 섹션

| # | ID | 영문 레이블 | 한국어 | 역할 |
|---|---|---|---|---|
| 0 | `#top` | Hero | — | 인상, 키 메시지, 메타 4종 |
| 1 | `#story` | Story | 소개 | 이름 의미(在訓), 자기소개 3단락 |
| 2 | `#capabilities` | Capabilities | 핵심 역량 | 4개 역량 카드 |
| 3 | `#projects` | Projects | 프로젝트 | 6개 프로젝트 (5완료+1WIP) |
| 4 | `#process` | How I Work | 일하는 방식 | 3단계 Process (DEFINE·IMPLEMENT·ITERATE) |
| 5 | `#experience` | Experience | 경험 | 4개 경험 카드 (증빙 첨부) |
| 6 | `#receipts` | Receipts | 검증된 성과 | 요약 3종 + 수상 이력 테이블 |
| 7 | `#log` | Log | 이력 타임라인 | 12개 타임라인 항목 (2017—2026) |
| 8 | `#contact` | Contact | 연락처 | 다크 블록, 이메일·전화, CTA |

---

## 5. 컴포넌트 카탈로그

### 5.1 고정 헤더 영역

```
[JH®]  [≡ Menu | ◑ | 00%]  [Get in touch ●]
 좌측 브랜드  중앙 Pill Nav     우측 CTA
```

- **Brand** (`.brand`): 고정 좌측, `JH` 검정 블록 + `®` 슈퍼스크립트
- **Pill Nav** (`.pill-nav`): 중앙 고정, `≡ Menu` 드롭다운 + 테마 토글(◑) + 스크롤 % 진행 표시
  - `.menu-panel`: 하단 드롭다운, 8개 섹션 링크, 한국어 서브레이블 우측 정렬
- **CTA Pill** (`.cta-pill`): 우측 고정, 오렌지 점(온라인 상태 표시 연상) + "Get in touch" 텍스트

### 5.2 태그 컴포넌트 (`.tag`)

```
● SECTION-NAME · 한국어
```

- 모노스페이스, 11px, letter-spacing .1em, 대문자
- 색상 변형: `.tag--orange`, `.tag--blue`, `.tag--white`

### 5.3 섹션 헤더 (`.sec-head`)

- 2컬럼 그리드: `1.4fr 1fr`
- 좌: `.tag` + 메인 타이틀 (`clamp(32px, 4.6vw, 64px)`)
- 우: 보조 설명 텍스트 (최대 380px)
- 모바일 900px 이하: 단일 컬럼 스택

### 5.4 역량 카드 (`.cap`)

- 4컬럼 → 2컬럼(900px) → 1컬럼(540px)
- 1px 헤어라인 테두리 그리드 (border-top + border-left 패턴)
- 호버: `--bg-soft` 배경 전환
- 구성: `cap__num` (오렌지 모노) + `cap__title` + `cap__desc`

### 5.5 프로젝트 카드 (`.proj`)

기본 구조:
```
[번호] [레이블 · 수상]              [연도]
[프로젝트 이름]
[서브타이틀]
[keywords — 토스 스타일 3줄]
[MY ROLE & INSIGHT ——]
[상세 설명]
[GitHub/외부 링크 버튼]     |  [이미지/비주얼]
```

**이미지 컨테이너 (`.proj__shot`)**:
- `aspect-ratio: 16/10` (기본 가로)
- `aspect-ratio: 9/16` (세로형, `.proj__shot--tall`)
- `object-fit: cover` + `object-position: center`
- 호버: `scale(1.04)` 줌인

**이미지 그리드**:
- `.proj__shots-grid`: 3컬럼, `9/16` 비율 (세로형 3장)
- `.proj__shots-grid--2`: 2컬럼, `16/10` 비율 (가로형 2장)

**다크 변형 (`.proj--dark`)**:
- 전체 섹션 배경 `var(--ink)`, 패딩 좌우로 full-bleed
- 텍스트/선/링크 모두 화이트 기반으로 전환

**플레이스홀더 (`.proj__placeholder`)**:
- `4/5` 비율, `var(--ink)` 배경
- 오렌지 방사형 그라디언트 오버레이
- 중앙에 `25:00` 오렌지 타이머 텍스트

### 5.6 프로세스 블록 (`.pblock`)

- 2컬럼 그리드: `80px 1fr` (번호 | 메인)
- 메인 내부: `1fr 1fr` (제목 | 설명+피처리스트)
- 상하 80px 패딩, 하단 1px 헤어라인 구분
- 피처리스트: `—` 오렌지 불릿

### 5.7 경험 카드 (`.exp`)

- 2컬럼 그리드 → 1컬럼 (720px)
- `--bg-elev` 배경, `--line` 테두리, `--r` 라운드
- 호버: `translateY(-3px)` + 테두리 `--ink`
- **증빙 섹션 (`.exp__cert`)**:
  - `data-lightbox="이미지경로"` → 클릭 시 라이트박스 오픈
  - YouTube 링크: `exp__cert--video` (빨간 아이콘)
  - 이미지: 48×60 썸네일

### 5.8 수상 테이블 (`.award`)

- 4컬럼 그리드: `110px 1.4fr 1.3fr 100px`
- 호버: `padding-left: 14px` 슬라이드 인
- `<em>` 태그로 수상 레벨 오렌지 강조

### 5.9 타임라인 (`.timeline`)

- `padding-left: 130px`, 왼쪽 오렌지→연한 그라디언트 1px 수직선
- `.tl::before`: 오렌지 테두리 도트 마커
- 호버: 마커 `scale(1.3)` + 오렌지 채움

### 5.10 컨택트 블록 (`.contact`)

- 전체 배경 `var(--ink)` (다크 반전)
- `border-radius: var(--r-lg)`, 좌우 마진 `var(--pad-x)`
- 거대 타이틀 `clamp(40px, 7vw, 112px)` + 오렌지 액센트
- 이메일/전화 카드 + PDF/HTML 다운로드 링크

---

## 6. 콘텐츠 인벤토리

### 6.1 인적사항

| 항목 | 값 |
|---|---|
| 이름 | 정재훈 (Jung Jaehun) |
| 생년 | 1998 |
| 이메일 | deephoony@gmail.com |
| 전화 | 010-8104-2425 |
| 학교 | 숭실대학교 전자정보공학부 |
| 전공 | IT 융합전공 · 스마트자동차 |
| 졸업 예정 | 2026.08 |
| 소재 | Seoul, Korea |

### 6.2 핵심 역량 4종

| 번호 | 제목 |
|---|---|
| 01 | 관행 타파, 맥락 기반 문제 정의 |
| 02 | 타인의 관점 체화와 이타적 설계 |
| 03 | 벽을 허무는 빠르고 책임 있는 구현력 |
| 04 | 팀워크와 타협을 이끄는 커뮤니케이션 |

### 6.3 프로젝트 6종

| # | 프로젝트명 | 연도 | 수상 | 이미지 | 링크 |
|---|---|---|---|---|---|
| 01 | 조달머신 | 2022 | 조달청 공공빅데이터 최우수상 | `jodal1.png`, `jodal2.png` | [GitHub](https://github.com/deephoon/JodalMachine) |
| 02 | 선배챗 | 2024.11 | GALA 2024 우수상 | `sunbaechat1.png`, `sunbaechat2.png`, `sunbaechat3.png` | [GALA 수상작](https://fastcampus.co.kr/gala2024_track1_04) |
| 03 | 따따 | 2025.02 | UMC 7기 최우수상 + Play Store 출시 | `ttatta1.png`, `ttatta2.png`, `ttatta3.png` | [GitHub](https://github.com/Ttatta-org/Ttatta_Android) |
| 04 | 슈토피아 (SSU:TOPIA) | 2025.02 | 숭실대 AI 아이디어톤 최우수상 | `shutopia1.png`, `shutopia2.png`, `shutopia3.png` | — |
| 05 | EV Fault Co-Pilot | 2025 | 졸업논문 (교내 내부 공개 제한) | `ev-thesis.png`, `ev1.png`, `ev2.png` | [GitHub](https://github.com/deephoon/EV-fault-GPT) |
| 06 | Tomato AI OS | 2025— | — (WIP) | CSS 플레이스홀더 (`25:00`) | — |

**주의**: 프로젝트 05(EV Fault)는 다크 배경(`.proj--dark`) 처리. 프로젝트 06는 이미지 미완성, CSS 플레이스홀더 사용.

### 6.4 경험 4종

| 기간 | 이름 | 역할 | 증빙 |
|---|---|---|---|
| 2020–2021 | 숭실대 중앙 밴드 동아리 SOMA | 회장 | YouTube 영상 링크 |
| 2021.07–현재 | 명품관 웰커밍 VIP 그리터 (JH Communication) | 명품관 그리터 | `career-cert.png` (라이트박스) |
| 2022.08 | 실리콘밸리 AI 온라인 인턴십 | 참가자 | `sv-cert.png` (라이트박스) |
| 2025.03–2025.09 | 구름톤 유니브 숭실대 4기 | 전체 부대표 & Android 파트장 | `goormthon-cert.png` (라이트박스) |

**중요**: 경험 섹션의 직책명은 반드시 **"명품관 웰커밍 VIP 그리터"** 로 표기.

### 6.5 수상 이력 4건

| 날짜 | 대회 | 프로젝트 | 등수 |
|---|---|---|---|
| 2025.02 | UMC 7기 데모데이 | 따따 | 전국 1위 (최우수상) |
| 2025.02 | 숭실대 AI 아이디어톤 | 슈토피아 | 교내 1위 (최우수상) |
| 2025.01 | 패스트캠퍼스 GALA 2024 | 선배챗 | 전국 우수상 |
| 2022.04 | 조달청 공공빅데이터 | 조달머신 | 전국 1위 (최우수상) |

---

## 7. 이미지 에셋 목록

위치: `images/` 디렉토리 (index.html 기준 상대경로)

| 파일명 | 용도 | 섹션 | 표시 방식 |
|---|---|---|---|
| `profile.png` | 프로필 사진 | Story | `aspect-ratio: 3/4`, object-fit cover |
| `jodal1.png` | 조달머신 화면1 | Projects #01 | 2컬럼 그리드, `16/10` |
| `jodal2.png` | 조달머신 화면2 | Projects #01 | 2컬럼 그리드, `16/10` |
| `sunbaechat1.png` | 선배챗 화면1 | Projects #02 | 3컬럼 그리드, `9/16` |
| `sunbaechat2.png` | 선배챗 화면2 | Projects #02 | 3컬럼 그리드, `9/16` |
| `sunbaechat3.png` | 선배챗 화면3 | Projects #02 | 3컬럼 그리드, `9/16` |
| `ttatta1.png` | 따따 화면1 | Projects #03 | 3컬럼 그리드, `9/16` |
| `ttatta2.png` | 따따 화면2 | Projects #03 | 3컬럼 그리드, `9/16` |
| `ttatta3.png` | 따따 화면3 | Projects #03 | 3컬럼 그리드, `9/16` |
| `shutopia1.png` | 슈토피아1 | Projects #04 | 3컬럼 그리드, `9/16` |
| `shutopia2.png` | 슈토피아2 | Projects #04 | 3컬럼 그리드, `9/16` |
| `shutopia3.png` | 슈토피아 상장 | Projects #04 | 3컬럼 그리드, `9/16` |
| `ev-thesis.png` | EV 논문 캡처 | Projects #05 | 단독 `16/10` |
| `ev1.png` | EV 시뮬레이터1 | Projects #05 | 2컬럼 그리드, `16/10` |
| `ev2.png` | EV 시뮬레이터2 | Projects #05 | 2컬럼 그리드, `16/10` |
| `career-cert.png` | 경력증명서 | Experience | 라이트박스 (48×60 썸네일) |
| `sv-cert.png` | 실리콘밸리 수료증 | Experience | 라이트박스 (48×60 썸네일) |
| `goormthon-cert.png` | 구름톤 수료증 | Experience | 라이트박스 (48×60 썸네일) |

모든 이미지에 `loading="lazy"` 적용.

---

## 8. 인터랙션 & JS 동작

### 8.1 스크롤 진행률

```js
window.addEventListener('scroll', () => {
  const p = Math.round((scrollTop / (scrollHeight - clientHeight)) * 100);
  progressEl.textContent = p + '%';
}, { passive: true });
```

### 8.2 메뉴 드롭다운

- `menu-btn` 클릭 → `.menu-panel`에 `.on` 클래스 토글
- `aria-expanded` 상태 동기화
- 메뉴 외부 클릭 시 자동 닫힘
- 메뉴 항목 클릭 시 닫힘

### 8.3 테마 토글

- `dark` 불리언 로컬 상태 (`let dark = false`)
- 클릭마다 CSS 변수 개별 setProperty
- **현재 미구현**: `localStorage` 저장 없음 (페이지 리프레시 시 라이트로 리셋)

### 8.4 스크롤 리빌 애니메이션

- `.reveal` 클래스: `opacity:0; transform:translateY(24px)`
- `IntersectionObserver` (`threshold: 0.1`, `rootMargin: '-5% 0px -5% 0px'`)
- 뷰포트 진입 시 `.in` 클래스 추가 → 트랜지션 발동
- `prefers-reduced-motion` 미디어쿼리로 모든 애니메이션 비활성화 지원

### 8.5 라이트박스

- `[data-lightbox="이미지경로"]` 속성을 가진 요소 클릭 시 전체화면 오버레이
- `body.overflow = 'hidden'` 으로 스크롤 잠금
- 클릭 또는 `Escape` 키로 닫힘
- 초기 `display:none` → `.on` 추가 시 `display:flex`

### 8.6 부드러운 스크롤

- `a[href^="#"]` 전체에 smooth scroll 적용
- 오프셋: `getBoundingClientRect().top + scrollY - 30`

---

## 9. 반응형 브레이크포인트

| 브레이크포인트 | 주요 변화 |
|---|---|
| `max-width: 900px` | `.sec-head` 단일 컬럼, `.story` 단일 컬럼, `.proj__row` 단일 컬럼, `.pblock__main` 단일 컬럼, `.caps` 2컬럼 |
| `max-width: 720px` | `.hero__meta` 2컬럼, `.pill-nav` / `.brand` / `.cta-pill` 축소, `.contact` 패딩 축소, `.exps` 단일 컬럼, `.timeline` 들여쓰기 축소, `.award` 랭크 열 숨김 |
| `max-width: 540px` | `.caps` 1컬럼 |

---

## 10. 기술 제약사항

- **빌드 툴 없음**: React, Vite, webpack 등 불가. 순수 HTML/CSS/JS.
- **외부 스크립트 없음**: jQuery, Alpine.js, GSAP 미사용. 바닐라 JS만.
- **폰트 CDN 의존**: Google Fonts + jsdelivr CDN 인터넷 연결 필요.
- **단일 파일**: 모든 CSS와 JS가 `<style>`, `<script>` 태그 안에 인라인.
- **이미지 로컬**: `images/` 폴더 필수. 외부 이미지 서비스 미사용.
- **PDF 파일**: `정재훈_이력서_경험기술서.pdf` 로컬 파일 다운로드 링크 있음.

---

## 14. 브랜드 카피 레퍼런스

- **Hero 타이틀**: "끊임없이 도전하고, 팀을 올바른 방향으로."
- **Hero 서브**: "개인의 뛰어남을 넘어 스스로 먼저 고민하고 팀의 기준을 설계합니다."
- **Contact 타이틀**: "데이터로 파악하고 공감으로 이끄는 다음 챕터."
- **Footer 이름 의미**: "在(있을 재) 訓(가르칠 훈) — 끊임없이 배움을 쥐고, 나누어 주며, 스스로 부딪히는 인생의 기록장."
- **Contact sub**: "숫자 이면의 사용자 맥락을 읽어내고, 가장 효율적인 기준을 세워 팀의 마찰을 줄이는 사람..."
- **이름 의미 뱃지**: `在 있을 재 · 訓 가르칠 훈`

---

## 15. 에이전트를 위한 작업 지침

이 명세서를 기반으로 작업하는 에이전트에 대한 지침:

1. **단일 파일 원칙**: 모든 변경은 `index.html` 하나 안에서 완결. 새 JS/CSS 파일 생성 금지.
2. **콘텐츠 정확성**: 프로젝트 설명을 과대해석하지 않는다. 특히 Tomato AI OS는 뽀모도로 타이머 WIP이며, 조달머신·선배챗·따따·슈토피아·EV Fault가 핵심 5개 프로젝트다.
3. **직책명 준수**: "명품관 웰커밍 VIP 그리터" — 백화점 웰커밍 그리터, 백화점 명품매장 그리터 등 오기 금지.
4. **색상 절제**: 새 색상 추가 금지. 오렌지(`#FF3E00`)는 액센트로만, 배경에 색상 블록 금지.
5. **CSS 변수 우선**: 하드코딩 색상값 대신 반드시 CSS 변수 사용.
6. **이미지 컨테이너 패턴**: 이미지 표시 시 반드시 `.proj__shot` + `aspect-ratio` + `object-fit:cover` 패턴 준수. 클립패스나 유기적 형태 사용 금지.
7. **접근성**: `aria-label`, `alt` 텍스트 유지. `prefers-reduced-motion` 쿼리 유지.
