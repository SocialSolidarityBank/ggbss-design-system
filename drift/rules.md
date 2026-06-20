# 드리프트 규칙 (린트)

토큰 규율 위반 = 드리프트. 라이브(`ggbss-web`)는 stylelint로 자동 집행하며, 이 문서는 그 규칙의 정본 참조다.

## 자동 집행 (stylelint)
| # | 규칙 | 위반 예 → 교정 |
|---|---|---|
| R1 | hex/rgb 색 리터럴 금지(생성 토큰 파일 제외) | `#006CB7` → `var(--c-primary)` |
| R2 | px/rem/em font-size 리터럴 금지 | `font-size: 16px` → `var(--fs-caption)` |
| R3 | **14px 미만 글자 금지** (`--fs-tagline` floor) | `font-size: 12px` → `var(--fs-tagline)` |
| R4 | font-family 리터럴 금지 | → `var(--ff)` / `var(--ff-en)` |
| R5 | Tailwind 임의값 색·폰트(`text-[#..]`·`text-[14px]`) 금지 | → 토큰 |

## 리뷰 집행 (자동 검사 밖)
| # | 규칙 |
|---|---|
| C1 | 간격은 `--sp-*`(4·8 배수)만. 어중간 px 금지 |
| C2 | 제목은 타입스케일 토큰만. 본문~h3 갭은 h4(24)/h5(20). 임의 20~36px 금지 |
| C3 | 한↔영 한 폰트(Pretendard) — 영문도 `--ff-en`=Pretendard 굵기 일치 |
| C4 | 한쪽만 강조 보더(`border-left` 단독) 금지 → 4면 또는 배경 틴트 |
| C5 | 제목 = `--c-ink-deep`(primary 파랑 아님), 버튼 = outline 기본(hover fill) |
| C6 | 그라디언트 = LIGHT×LIGHT만. primary/dark-blue/ink-deep 간 그라디언트 금지 |
| C7 | italic 금지 — 강조는 굵기/색으로 |

## 고정-다크 예외 (린트 통과시키되 주석 필수)
항상 어두운 표면(반전 카드·band·스크림·코드블록·다크 글래스)의 `#0a1e33`/`#fff`/`rgba(10,30,51,..)` 리터럴은 **의도된 것** → 유지하고 `/* intentional: fixed-dark */` 주석. 이걸 토큰화하면 `[data-theme="dark"]`에서 깨진다.

## 검사
```bash
# 라이브 레포에서
cd ggbss-web/web && stylelint "app/**/*.css"   # exit 0 = 통과 (hex 경고는 고정-다크 예외 검토)
```
드리프트 발견 시: **위반**(규칙 어김)→교정 / **공백**(토큰 부재로 임의 구현)→`tokens.css` 토큰 추가 / **결함**(규칙이 현실과 불일치)→매뉴얼 개정 + 사용자 승인.
