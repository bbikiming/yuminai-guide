# 04 — 시각 아이덴티티 (Visual Identity)

> 가이드 디자인을 앱과 일치시키기 위한 모든 토큰. 디자이너가 그대로 쓸 수 있는 hex/spec.

## 브랜드 색상

### Primary — 앱 아이콘 그라디언트
> 보라 → 인디고 → 파랑

| 토큰 | Hex | 용도 |
|------|-----|------|
| `brand.purple` | `#7C3AED` | 그라디언트 시작 (Y 좌상단) |
| `brand.indigo` | `#5B5DEF` | 그라디언트 중간 |
| `brand.blue` | `#3B82F6` | 그라디언트 끝 (Y 우하단) |
| `brand.purple-dark` | `#8B5CF6` → `#6366F1` | Triangle accent |
| `brand.lavender` | `#A78BFA` | Outline + circuit lines (35% opacity) |
| `brand.sky` | `#60A5FA` | 우측 outline + circuit |

### UI Accent — Theme.Brand.accent
> AG2R La Mondiale 자전거 팀 시그니처 시안

| 토큰 | Hex | 용도 |
|------|-----|------|
| `accent` | `#22C8E0` | CTA, active state, link, streaming, selected |
| `accentDeep` | `#0FA8C0` | Hover state |
| `accentMuted` (light) | `#D4F2F8` | 사용자 메시지 배경 (light mode) |
| `accentMuted` (dark) | `#0A2128` | 사용자 메시지 배경 (dark mode) |
| `accentBorder` | `#22C8E0` @ 45% | Accent border |

### Agent 색상 (ADR-087)

| Agent | 색상 | Hex | Muted (light) | Muted (dark) |
|-------|------|-----|---------------|---------------|
| **Claude** | Anthropic 오렌지 | `#D97706` | `#FEF3C7` | `#4A2D08` |
| **Codex** | OpenAI 틸그린 | `#10A37F` | `#D1FAE5` | `#064237` |

→ Composer 좌측 strip, 통합 picker, handoff chip, 메시지 마커에 사용

## 표면 (Surface) — 4단 hierarchy

### Dark mode (default)

| 토큰 | Hex | 용도 |
|------|-----|------|
| `bgSidebar` | `#161514` | 사이드바 배경 (가장 어두움) |
| `bg` | `#1A1817` | 메인 배경 (chat 본문) |
| `surface` | `#211F1D` | 카드/sheet 표면 |
| `surfaceHi` | `#2A2724` | hover/elevated |
| `elevated` | `#322E2A` | popover/menu |

### Light mode

| 토큰 | Hex | 용도 |
|------|-----|------|
| `bgSidebar` | `#EEEBE6` | 사이드바 배경 |
| `bg` | `#F6F3EE` | 메인 배경 (warm) |
| `surface` | `#FFFEFB` | 카드/sheet 표면 |
| `surfaceHi` | `#E8E4DD` | hover/elevated |

> **포인트**: warm 다크 (#161514 등 brown-tinted black)이 차가운 black이 아닌 점.

## 텍스트 (WCAG 2.2 AA 검증됨)

### Dark mode

| 토큰 | Hex | 대비 (vs `bg`) |
|------|-----|--------------|
| `text` | `#F0EEEC` | 14.2:1 (AAA) |
| `textSecondary` | `#A8A3A0` | 7.8:1 (AAA) |
| `textTertiary` | `#8E8884` | **4.85:1 (AA)** ← ADR-072에서 명시적으로 fix |
| `textDisabled` | `#5A5552` | 2.5:1 (deco only) |

### Light mode

| 토큰 | Hex |
|------|-----|
| `text` | `#1A1817` |
| `textSecondary` | `#5A5552` |
| `textTertiary` | `#6B6663` (5.00:1 AA) |

## 상태 색

| 토큰 | Hex | 용도 |
|------|-----|------|
| `success` | `#8FC999` | 성공, diff plus, healthy |
| `warning` | `#D4B86A` | 경고 |
| `danger` | `#D97373` | 에러, diff minus, 삭제 버튼 |
| `liveDot` | `#22C8E0` (= accent) | 스트리밍 중 펄스 |

## 폴더 색상 (ADR-077)

`folderColor(for: name)` — semantic name → SwiftUI Color:

`accent` · `blue` · `purple` · `pink` · `red` · `orange` · `yellow` · `green` · `teal` · `gray`

## 타이포그래피

> SF Pro (sans) + SF Mono (code) — 시스템 default. 별도 webfont 불필요.

### Sans (본문)

| 토큰 | size | weight | 용도 |
|------|------|--------|------|
| `display` | 22 | semibold | 페이지 타이틀 |
| `title` | 17 | semibold | sheet 타이틀, 섹션 헤더 |
| `body` | 14 | regular | 본문 default |
| `bodyEmphasis` | 14 | medium | 본문 강조 |
| `label` | 13 | medium | 버튼/picker 라벨 |
| `small` | 12 | regular | 보조 설명 |
| `micro` | 11 | medium | 캡션, 메타 |

### Mono (code, stats, breadcrumb)

| 토큰 | size | weight | 용도 |
|------|------|--------|------|
| `mono` | 13 | regular | 일반 코드 |
| `monoSmall` | 12 | medium | branch name, stats |
| `monoStat` | 18 | semibold | 큰 숫자 (대시보드) |
| `codeBlock` | 12 | regular | 코드 블록 |

### 가이드 사이트 추천 매핑 (디자이너용)

| 가이드 요소 | Theme 토큰 |
|------------|-----------|
| H1 (챕터 제목) | `display` (22pt semibold) → 가이드는 32~48pt까지 키워도 OK |
| H2 (섹션) | `title` (17pt semibold) → 24pt 권장 |
| H3 (서브섹션) | `bodyEmphasis` (14pt medium) → 18pt 권장 |
| 본문 | `body` (14pt) → 16pt 권장 (가이드는 더 읽기 편하게) |
| 코드/단축키 | `mono` 또는 `monoSmall` |
| 캡션 | `micro` (11pt) → 12pt 권장 |

## Spacing — 4의 배수

| 토큰 | 값 |
|------|-----|
| `xxs` | 2 |
| `xs` | 4 |
| `sm` | 8 |
| `md` | 12 |
| `lg` | 16 |
| `xl` | 24 |
| `xxl` | 32 |
| `xxxl` | 48 |

## Radius

| 토큰 | 값 | 용도 |
|------|-----|------|
| `none` | 0 | — |
| `sm` | 4 | 작은 chip, badge |
| `md` | 6 | 버튼, picker |
| `lg` | 8 | 카드, 메시지 박스 |
| `xl` | 12 | sheet, composer |
| `pill` | 999 | health pill, capsule |

## Stroke

| 토큰 | 값 | 용도 |
|------|-----|------|
| `hairline` | 1 | border |
| `bar` | 2 | 선택된 사이드바 항목 좌측 accent |

## 레이아웃

### 메인 윈도우

| 영역 | 너비 | 비고 |
|------|------|------|
| Sidebar | 280pt (default), 220~360pt | minimum 220 |
| Inspector | 300pt (default), 240~420pt | minimum 240 |
| Chat content | min 460pt, max 820pt | center-aligned (`contentMaxWidth`) |
| Toolbar | 44pt 높이 | |
| Status bar | 28pt 높이 | |
| Composer | 104~320pt 높이 | 자동 grow |

### 윈도우 최소 크기 (ADR-070)

- 최소 너비: **460pt** (보조 모니터 960px 모니터에서 2-up 가능)
- 최소 높이: **360pt**

### Sheet 사이즈 (ADR-073, 074)

- Settings sheet: ideal 720×560, min 460×360
- 일반 sheet: 모두 `absoluteMinWidth=360`, 부모 윈도우의 `0.92ratio`까지 자동 축소
- 큰 화면에서는 스크롤 없이 보이도록 ideal size 자동 적용

### Layout breakpoints (ADR-070)

| Mode | 너비 | 변화 |
|------|------|------|
| `tiny` | < 600 | toolbar 일부 숨김, sidebar overlay |
| `compact` | 600~760 | sidebar overlay only, inspector hidden |
| `medium` | 760~1080 | sidebar inline, inspector hidden |
| `regular` | 1080~1440 | sidebar inline, inspector 옵션 |
| `wide` | ≥ 1440 | 모두 inline |

## 애니메이션

| 토큰 | 값 |
|------|-----|
| `stateChange` | `.easeOut(duration: 0.12)` |
| `panelToggle` | `.easeInOut(duration: 0.18)` |
| `pulseDuration` | 1.5s |

## 앱 아이콘 — 디자인 컨셉 (ADR-086)

> "Convergence + Code" — 멀티 에이전트 (Y 형태로 수렴) + 개발 환경 (`< >` arrows + circuit)

### 구조 (1024×1024)

1. **흰색 squircle** — Apple Big Sur+ spec (824×824, 180 corner radius, 100px padding)
2. **Outer circle outline** — orbital ring (lavender→sky 그라디언트, 45% opacity)
3. **Orbital dots** — 12/3/6/9 시 방향, 4개 (보라/인디고/파랑/인디고)
4. **Top triangle accent** — focus/play 메타포 (보라 짙은→밝은 그라디언트)
5. **Y shape** — 보라→파랑 그라디언트 (Yuminai의 "Y" + multi-agent → unified)
6. **Left/Right arrows** (`<` `>`) — CLI / code editor 메타포
7. **Subtle circuit lines** — 좌우 밑변 + 상단 (lavender 30~35% opacity)

### iconset 사이즈

10개 표준 size: 16, 16@2x, 32, 32@2x, 128, 128@2x, 256, 256@2x, 512, 512@2x

→ `assets/AppIcon.svg` 파일 동봉. 가이드 표지/로고 자산으로 활용 가능.

## 디자인 원칙 (가이드에도 적용)

1. **Claude Code 본능 보존** — 슬래시 명령, 키보드 전부, 다크 다크 다크
2. **Liquid Glass는 chrome에만** — 사이드바·툴바·패널 분할에 적용, 채팅 본문엔 미적용 (가독성)
3. **Monospace는 코드에만** — UI 텍스트는 SF Pro, 코드/Claude 출력은 SF Mono
4. **마우스 < 키보드** — 모든 액션이 단축키로 가능
5. **밀도 우선** — 1인 사용이라 "친절한 여백"보다 "한 화면 더 보이는 것"

## 가이드 사이트 토큰 매핑 (web 권장 변환)

```css
:root {
  /* Brand */
  --brand-purple: #7C3AED;
  --brand-indigo: #5B5DEF;
  --brand-blue: #3B82F6;
  --brand-gradient: linear-gradient(135deg, #7C3AED 0%, #5B5DEF 50%, #3B82F6 100%);

  /* Accent */
  --accent: #22C8E0;
  --accent-deep: #0FA8C0;

  /* Agents */
  --agent-claude: #D97706;
  --agent-codex: #10A37F;

  /* Surfaces (dark default) */
  --bg: #1A1817;
  --bg-sidebar: #161514;
  --surface: #211F1D;
  --surface-hi: #2A2724;

  /* Text */
  --text: #F0EEEC;
  --text-secondary: #A8A3A0;
  --text-tertiary: #8E8884;

  /* Status */
  --success: #8FC999;
  --warning: #D4B86A;
  --danger: #D97373;

  /* Type — system stack */
  --font-sans: -apple-system, BlinkMacSystemFont, "SF Pro Text", system-ui, sans-serif;
  --font-mono: "SF Mono", ui-monospace, Menlo, Monaco, Consolas, monospace;
}
```
