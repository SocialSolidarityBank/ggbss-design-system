# GGBSS Design System

ggbss.or.kr(함께만드는세상 — 사회연대은행 부설) 본·서브도메인이 공유하는 **라이브 디자인 시스템의 단일 진실원(SSOT)**.

> ⚠️ **`BSS Design System`(shadcn 기반 별도 레포)과는 다른 시스템**입니다. GGBSS는 실제 운영 중인 ggbss.or.kr의 CSS 변수 + CSS Modules 기반 시스템을 정본화한 것으로, 두 시스템은 *아이디어가 다르므로* 통합하지 않고 별도 관리합니다.

## 무엇인가
- 라이브 사이트(`ggbss-web`)에서 추출·정규화한 토큰·규칙·컴포넌트 카탈로그.
- 사람이 읽는 매뉴얼이자, **Claude Design / Claude Code가 GitHub-import 해 일관 적용**할 수 있는 가져오기용 SSOT.

## 구조
```
tokens/
  tokens.css     # 색·타입스케일·간격·반경·그림자·라인·그라디언트 + 다크 플립 (base SSOT)
  globals.css    # semantic alias·버튼 기본·base reset·다크 재고정
docs/
  design.md      # 정본 매뉴얼 (원칙·surface matrix·다크모드·금지 규칙)
  components.md  # 27개 컴포넌트 카탈로그
drift/
  rules.md       # 토큰 규율 린트 규칙 (min-14·리터럴 금지·그리드)
```

## 타입 스케일 (8-grid, 2026-06-20 정규화)
| 토큰 | px | 용도 |
|---|---|---|
| `--fs-h1` | 64 | 히어로 |
| `--fs-h2` | 56 | 페이지 대제목 |
| `--fs-h3` | 40 | 섹션·페이지 제목 |
| `--fs-h4` | 24 | 카드·패널 제목 |
| `--fs-h5` | 20 | 소제목 |
| `--fs-body` | 18 | 본문 |
| `--fs-caption` | 16 | 캡션·표 셀·컨트롤 |
| `--fs-tagline` | 14 | 라벨·칩 (최소 폰트 floor) |
| `--fs-display` | 48 | 점수·대표 수치 |
| `--fs-stat` / `-lg` | 34 / 38 | data 대시보드 통계 |

## 사용 / 가져오기
1. **Claude Design**: 이 레포를 design-system 프로젝트로 import → 모든 작업에 자동 적용.
2. **Claude Code**: `/design-sync`로 컴포넌트 단위 동기화.
3. **사람**: `docs/design.md`가 정본 매뉴얼.

## 정본 소스
라이브 구현체는 `ggbss-web` 레포의 `web/app/_v2/tokens.css`·`web/app/globals.css`·`web/app/(chrome)/design/**`. 이 레포는 그 정규화 스냅샷이며, 변경은 라이브 → 이 레포 순으로 반영한다.
