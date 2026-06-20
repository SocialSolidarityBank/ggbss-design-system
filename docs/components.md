# 컴포넌트 카탈로그

라이브 쇼케이스: **design.ggbss.or.kr/design/components/{name}** · 소스: `ggbss-web` `web/app/(chrome)/design/components/{name}/`. 전 컴포넌트 토큰 기반(`CLAUDE.md` 규율 준수).

## 컨트롤 / 폼
| 컴포넌트 | 용도 |
|---|---|
| `button` | 기본 outline, hover 시 fill. 반경 `--r-ctl`(8), 본문 `--fs-button`(16) |
| `input` | 텍스트 입력. line 토큰(default→hover ink-deep→focus primary), inset shadow로 hover/focus 두께 |
| `select-controls` | select·checkbox·radio·switch |
| `fieldset` | 폼 그룹 컨테이너 |
| `search` | 검색 입력(돋보기 컨벤션) |
| `keyboard` | 키캡(kbd) 표시 |

## 컨테이너 / 표면
| 컴포넌트 | 용도 |
|---|---|
| `card` | 기본 카드. 반경 `--r-xl`(16), 제목 `--fs-h4`(24) |
| `context-card` | 맥락 정보 카드 |
| `doc-card` | 문서·자료 카드 |
| `section` | 섹션 래퍼(한 섹션 한 목적) |
| `hero` | 히어로(워시 그라디언트 `--gr-wash-hero`, 다크 자동 플립) |
| `entity` | 엔티티/프로필 표시 |

## 데이터
| 컴포넌트 | 용도 |
|---|---|
| `table` | 표. th `--c-light-grey` 틴트(다크=sky 틴트 플립), 셀 `--fs-caption`(16) |
| `gauge` | 반원 SVG 게이지. 중앙값 `--fs-h5`/800, 라벨 14px(굵기·색으로 위계) |
| `calendar` | 달력 |

## 피드백 / 오버레이
| 컴포넌트 | 용도 |
|---|---|
| `notice` | 인라인 알림(semantic 색) |
| `feedback` | 성공/오류 피드백 |
| `tooltip` | 툴팁 |
| `drawer` | 사이드 드로어(스크림 `rgba(10,30,51,.35)` 고정-다크) |
| `menu` | 드롭다운 메뉴 |
| `command-menu` | ⌘K 커맨드 팔레트 |
| `floating-cta` | 플로팅 CTA |

## 내비게이션 / 구조
| 컴포넌트 | 용도 |
|---|---|
| `nav-flyout` | 데스크톱 캐스케이딩 플라이아웃 |
| `accordion` | 아코디언(hairline divider) |
| `file-tree` | 파일 트리(.ext 칩 `--fs-tagline`) |

## 콘텐츠
| 컴포넌트 | 용도 |
|---|---|
| `badge` | 상태/카테고리 pill(semantic 틴트). `chip`=액션 칩 |
| `code-block` | 코드 블록(항상 어두운 표면) |

## 파운데이션 문서
색 `/design/colors` · 타입 `/design/typography` · 간격 `/design/spacing` · 반경 `/design/radius` · 엘리베이션 `/design/elevation` · 표면 `/design/surfaces` · 그라디언트 `/design/gradients` · 다크모드 `/design/dark-mode` · 레이아웃 `/design/layout-system` · 원칙 `/design/principles` · 패턴 `/design/patterns`.
