# DESIGN.md — sungjinbae.github.io

> 이 파일은 사이트의 모든 페이지 제작·수정 시 AI 코딩 에이전트가 따라야 하는 디자인 기준서다.
> 무드: **차분한 학술 사이트.** Valtorta의 정돈·색 일관성 + kantwon의 원페이지 스크롤 전개 + Stanford식 스크롤스파이. 화려함보다 신뢰감. 요소를 더하기보다 뺀다.

## 1. Color Tokens

라이트 모드 단일. 액센트는 **한 색**만 쓴다. 아래 토큰 외 색 사용 금지.

```css
:root {
  --bg:            #FAF9F7;  /* 따뜻한 종이 화이트 — 페이지 배경 */
  --surface:       #FFFFFF;  /* 카드·내비 배경 */
  --ink:           #1F2328;  /* 본문 텍스트 */
  --ink-soft:      #5A6169;  /* 보조 텍스트, 캡션, 날짜 */
  --accent:        #2C6E63;  /* 딥 틸 — 링크, 현재 섹션, 버튼 */
  --accent-strong: #1F5249;  /* hover/active */
  --accent-tint:   #EAF1EF;  /* 액센트 배경 틴트 — 태그, hover 배경 */
  --line:          #E7E4DE;  /* 헤어라인 보더 */
}
```

규칙: 순수 검정(#000)·순수 흰 배경(#FFF full-bleed) 금지. 그라디언트 금지. 그림자는 `0 1px 2px rgb(0 0 0 / 4%)` 한 단계만.

## 2. Typography

```css
--font-display: "Source Serif 4", "Noto Serif KR", Georgia, serif;   /* 이름, 섹션 타이틀 */
--font-body:    "Inter", "Pretendard", -apple-system, sans-serif;    /* 본문 */
--font-mono:    "JetBrains Mono", monospace;                          /* 연도, 라벨, 넘버링 */
```

| 용도 | 크기 | 무게 | 폰트 |
|---|---|---|---|
| Hero 이름 | clamp(44px, 7vw, 76px) | 600 | display |
| 섹션 타이틀 (H2) | 32px | 600 | display |
| 서브타이틀 (H3) | 20px | 600 | body |
| 본문 | 17px / line-height 1.7 | 400 | body |
| 캡션·메타 | 14px | 400 | body, `--ink-soft` |
| 라벨·연도 | 13px, letter-spacing 0.06em, uppercase | 500 | mono, `--accent` |

본문 문단 폭 최대 68ch. 제목은 두 줄 이내로 유지.

## 3. Spacing & Layout

- 베이스 단위 4px. 스페이싱 스케일: 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 128
- 섹션 수직 패딩: 데스크톱 112px, 모바일 72px
- 콘텐츠 최대폭: 1040px (본문 프로즈는 720px), 좌우 패딩 24px
- 그리드: 프로젝트 카드 2열(모바일 1열), gap 32px
- radius: 카드·이미지 10px, 버튼·필 999px(pill)

## 4. Components

### Nav (상단 고정)
- 높이 64px, `--surface` + `backdrop-filter: blur(8px)`, 하단 `--line` 헤어라인. 스크롤 전(히어로 위)에는 투명
- 좌: "Sungjin Bae" (display 500). 우: About · Research · Publications · CV · Contact
- **스크롤스파이**: 현재 섹션 링크에 `--accent` 색 + 2px 언더라인. 부드럽게 이동(smooth scroll)

### Hero (첫 화면, 100svh)
- 구성: 이름(초대형 serif) → 한 줄 정체성 → 소속 한 줄(`--ink-soft`) → 링크 아이콘(Email·Scholar·LinkedIn·GitHub) → 하단 스크롤 큐(↓, 미세 바운스)
- 배경은 `--bg` 그대로. 이미지·그라디언트·파티클 금지. 임팩트는 타이포와 여백으로

### Section Header
- mono 라벨(예: `01 — RESEARCH`) + H2. 아래 48px 여백

### Publication Item (Valtorta식 정돈)
- 한 줄 구조: [연도 mono] 제목(600) — 저자(본인 굵게) — *저널/학회(이탤릭, ink-soft)* — 링크 필 [PDF] [DOI] [BibTeX]
- 필 버튼: `--accent-tint` 배경 + `--accent` 텍스트, hover 시 반전. 항목 hover: 배경 `--accent-tint` 30%
- 연도 역순 그룹핑. 유형 필터(Journal / Conference / Patent)는 상단 필 탭

### Project Card
- 상단 데모 GIF/영상(16:10, radius 10px, `--line` 보더) + 제목 + 2줄 요약 + "Read more →"(accent)
- 이미지 없는 카드 금지 — 로봇 연구는 반드시 움직이는 미디어

### Footer
- 헤어라인 위, 좌 카피라이트 / 우 링크 반복. 높이 최소화

## 5. Motion

- 원칙: **차분함.** duration 200–300ms, `ease-out`, 이동거리 ≤ 12px
- 섹션 진입 시 1회 fade-up(opacity 0→1, translateY 12px→0), stagger 60ms
- hover 전환 150ms. 패럴랙스·자동재생 캐러셀·스크롤 하이재킹 금지
- `prefers-reduced-motion: reduce` 시 모든 모션 제거

## 6. Do / Don't

**Do**: 여백으로 위계 만들기 · 모든 언급 항목에 링크(plopes 원칙) · 이미지 비율 통일 · 시맨틱 HTML(nav/section/article) · 라이트하우스 성능 90+
**Don't**: 액센트 외 색 추가 · 두 가지 이상 그림자 · 아이콘 남발 · 스톡 일러스트 · 3개 이상 폰트 · 팝업/배너

## 7. Accessibility & Meta

- 대비: 본문 4.5:1 이상 (`--ink` on `--bg` 충족), 액센트 텍스트는 16px 이상에서만
- 키보드 포커스 링: `2px solid var(--accent)` offset 2px
- OG 이미지: 이름+타이틀을 `--bg`/`--ink`로 조판한 1200×630
- favicon: 이니셜 "SB"를 `--accent` 원 안에
