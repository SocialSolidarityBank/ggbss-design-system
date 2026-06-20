# GGBSS 디자인 시스템 — 에이전트 가드레일

이 시스템으로 화면/컴포넌트를 만들 때 **반드시** 지킨다. 어기면 드리프트. 정본 매뉴얼 = `docs/design.md`, 토큰 SSOT = `tokens/tokens.css`.

## 1. 토큰만 (리터럴 금지)
색·글자크기·간격·반경·그림자·글꼴은 **토큰 var 참조만**:
- 색 → `var(--c-*)` (hex/rgb 리터럴 금지)
- 글자크기 → `var(--fs-*)` (px 리터럴 금지)
- 간격 → `var(--sp-*)` (4/8 그리드만)
- 반경 → `var(--r-*)`
- 글꼴 → `var(--ff)`(Pretendard) / `var(--ff-en)`(Satoshi)

**최소 폰트 = `--fs-tagline`(14px). 14px 미만 금지** (stylelint 집행).

## 2. 타입 스케일 (8-grid, 불변)
h1 64 · h2 56 · h3 40 · h4 24 · h5 20 · body 18 · caption 16 · tagline 14 · display 48 · stat 34/38.
- 본문~h3 사이 제목은 h4(24)/h5(20)로. 임의 20~36px 금지.
- 자간 `--tracking` = -0.01em (한↔영 통일). monospace(IP·도메인·코드)만 0.

## 3. 색 규율
- 제목 = `--c-ink-deep` (절대 primary 파랑 아님).
- 에러/위험 = `--c-danger`(순수 빨강), 경고 = `--c-warning`(주황).
- 랭크·배지 = `--c-rank-*`/`--c-badge-*` 토큰.
- **다크모드는 `[data-theme="dark"]`에서 base `--c-*`가 자동 플립** → 색은 토큰 참조만 하면 자동 대응.
  - **예외: 항상 어두운 표면**(반전 카드·band·스크림·코드블록·다크 글래스)은 `#0a1e33`/`#fff` 리터럴 유지 + `/* intentional: fixed-dark */` 주석. (토큰화하면 다크에서 깨짐)

## 4. 레이아웃
- 간격 = `--sp-*`(4·8 배수)만. 어중간 px 금지.
- 반경 = `--r-xs/sm/ctl/md/lg/xl/2xl/pill`. 버튼·컨트롤 = `--r-ctl`(8).
- 한쪽만 강조 보더(`border-left` 단독) 금지 → 4면 보더 또는 배경 틴트. (풀폭 divider `border-top/bottom`은 허용)

## 5. 컴포넌트
- 정의된 컴포넌트(`docs/components.md`)와 variant만 사용. 임의 그림자·반경·색 금지.
- 카드는 *카드가 곧 인터랙션*일 때만. 장식용 카드 그리드 금지.
- 한 섹션 = 한 목적. 가독 본문 폭 제한(full-bleed 본문 금지).

## 6. 스트랭글러
신규·수정 화면만 이 규칙을 강제. 기존 화면 일괄 교체 금지.

## 7. 자가검증
작업 후 `drift/rules.md` 기준 점검: 리터럴 색/px-폰트 0, 14px 미만 0, 토큰만. 라이브(`ggbss-web`)에선 `stylelint "app/**/*.css"` exit 0.

## 8. AI 슬롭 금지
보라 그라디언트·아이콘 원형칩 3단 그리드·전체 center 정렬·균일 bubbly 반경·장식 blob·이모지 장식·`border-left` 컬러칩·"Welcome to…" 카피·system-ui 본문폰트 → 전부 금지.
