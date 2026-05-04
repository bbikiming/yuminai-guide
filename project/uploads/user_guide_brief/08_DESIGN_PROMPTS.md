# 08 — 클로드 디자인 프롬프트 모음

> 클로드 디자인(또는 다른 AI 디자인 도구)에 **그대로 복사·붙여넣기** 가능한 프롬프트 8개.
> 첫 줄에 사용 시점, 본문에 프롬프트, 마지막에 첨부할 파일 표시.

---

## 프롬프트 #1 — 전체 가이드 사이트 (한 번에)

> **사용 시점**: 시간 절약 우선, 한 번에 끝내고 싶을 때
> **첨부 파일**: 이 폴더 전체 (8개 .md + AppIcon.svg)

```
한국 macOS 앱 "Yuminai"의 사용자 가이드 웹사이트를 디자인해줘.

# 제품 개요
Yuminai는 솔로 풀스택 개발자를 위한 macOS 데스크톱 앱이야. Claude Code와 OpenAI Codex CLI를
GUI 채팅으로 감싸고, Obsidian Vault, Telegram Bot, Git을 한 화면에서 통합한 "바이브 코딩"
워크스페이스야. 첨부한 8개 마크다운에 비전·페르소나·기능·시각 토큰·화면 구조·단축키·
가이드 목차가 다 들어 있어.

# 디자인 요구사항
- 톤: 미니멀, 다크 모드 default, 밀도 높음 (1인 도구라 친절한 여백 X)
- 언어: 한국어 ~합니다/~해요 톤
- 브랜드 색상: 보라(#7C3AED) → 인디고(#5B5DEF) → 파랑(#3B82F6) 그라디언트 (Y 모양 앱 아이콘)
- UI accent: cyan #22C8E0
- Agent 색상: Claude=오렌지(#D97706), Codex=틸그린(#10A37F)
- 폰트: SF Pro (sans), SF Mono (code/단축키)
- 04_VISUAL_IDENTITY.md의 모든 토큰을 시각에 일관 적용

# 가이드 구조 (07_USER_GUIDE_OUTLINE.md의 10챕터)
0. Welcome (히어로 + 1줄 정의)
1. Getting Started (설치 → 첫 워크스페이스 → 첫 메시지)
2. Workspaces (핀, 폴더, smart filter)
3. AI와 대화하기 (Composer, mention, multi-pane)
4. Claude ⇄ Codex (통합 picker, handoff)
5. 노트와 코드 연결 (Obsidian)
6. 모바일에서 명령 (Telegram, multi-bot)
7. 버전 관리 (Git, AI commit, PR)
8. 비용·생산성 트래킹 (Usage Dashboard)
9. 고급 (Plan mode, Harness, Multi-agent routing)
부록 A. 단축키 cheat sheet
부록 B. 트러블슈팅
부록 C. 글로서리

# 산출물
- 다크 default + 라이트 토글 가능
- 좌측 sticky ToC (10챕터)
- 각 챕터: 카드 기반 레이아웃, 2~4 페이지
- 헤더에 큰 앱 아이콘 (AppIcon.svg 활용)
- 단축키는 키 캡 형태로 표시 (예: ⌘N)
- 코드 블록은 SF Mono + 어두운 배경
- 모바일 반응형 (1024px 이하에서 ToC를 햄버거)
- 챕터 간 prev/next 네비게이션

# 산출물 우선순위
1. Welcome 페이지 (히어로) — 가장 중요
2. ToC + 챕터 0~3 (Getting Started, Workspaces, AI 대화) — 핵심
3. 챕터 4~9 — 후순위 OK

산출물 형태: HTML + CSS (single file 또는 챕터별 분리), 또는 React 컴포넌트.
```

---

## 프롬프트 #2 — Welcome / 히어로 페이지만

> **사용 시점**: 표지 한 장이 필요할 때
> **첨부 파일**: `01_PRODUCT_BRIEF.md`, `04_VISUAL_IDENTITY.md`, `assets/AppIcon.svg`

```
Yuminai 앱의 사용자 가이드 표지(히어로 페이지)를 디자인해줘.

Yuminai는 솔로 풀스택 개발자를 위한 macOS 앱으로, Claude Code와 OpenAI Codex를 한 화면에서
오케스트레이션하는 "바이브 코딩" 워크스페이스야. 첨부 SVG가 앱 아이콘이고, 보라→파랑
그라디언트 Y 모양이 시그니처 비주얼이야.

# 요구
- 다크 모드 (배경 #1A1817, 텍스트 #F0EEEC)
- 큰 앱 아이콘 (160×160 또는 더 크게) — SVG 그대로 또는 글로우 효과
- 워드마크 "Yuminai" — SF Pro Display Semibold, 48pt+
- 1줄 정의 (한국어): "바이브 코딩을 위한 1인 macOS 워크스페이스"
- 슬로건 후보 중 선택: "한 화면, 모든 코딩 사이클" / "Claude를 터미널 밖으로"
- "Get Started" 버튼 (cyan #22C8E0 accent) + "단축키 보기" (subtle)
- 하단에 키 워크플로우 아이콘 4개 한 줄: Claude · Codex · Obsidian · Telegram (각자 색상)
- 백그라운드: subtle 보라/파랑 그라디언트 글로우 (앱 아이콘 색상 reflection)

# 톤
미니멀, 어두운 우아함, "프로 개발자 도구" 느낌. Linear / Raycast / Cursor의 표지에 가깝게.

산출물: HTML + CSS (single page, responsive) 또는 React.
```

---

## 프롬프트 #3 — Getting Started (3 페이지)

> **사용 시점**: 첫 사용자 온보딩 가이드 챕터
> **첨부 파일**: `02_PERSONA_AND_USE_CASES.md`, `05_SCREEN_BY_SCREEN.md`

```
Yuminai 사용자 가이드의 "Getting Started" 챕터 3페이지를 디자인해줘.

# 페이지 1 — 설치 + 첫 실행
- macOS 26 + Claude CLI 사전 셋업 안내
- 다운로드/설치 절차 (간단)
- 첫 실행: Onboarding Wizard 3-step (Welcome → 모드 선택 → CLI 확인)
- 모드 선택 카드 3개: 🌱 초보자 · 🚀 고급 · 🎨 사용자 정의

# 페이지 2 — 첫 워크스페이스
- "⌘N" 키 캡 + 워크스페이스 생성 sheet 스크린샷
- 디렉토리 picker → 하네스 템플릿 선택 (5가지)
- 사이드바에 첫 항목 등장하는 시퀀스

# 페이지 3 — 첫 메시지
- Composer 좌측 오렌지 strip = Claude 사용 중
- 메시지 입력 + ⌘+Return 전송
- Claude 답변 스트리밍 GIF (또는 시퀀스)
- "축하합니다! 이제 ..." 마무리

# 톤
- 친절한데 길지 않게. 5분 안에 끝나는 가이드.
- "5분이면 끝나요" 같은 시간 약속 강조
- 다크 default, 한국어 ~해요 톤

# 시각
- 단축키는 실제 키 캡 그래픽
- 워크플로우 화살표 다이어그램
- screenshot 영역은 placeholder OK (나중에 실제 캡처 삽입)

산출물: HTML + CSS, 페이지 간 이동 prev/next 버튼.
```

---

## 프롬프트 #4 — Claude ⇄ Codex 챕터 (가장 차별화된 기능)

> **사용 시점**: 핵심 차별화 기능 디자인
> **첨부 파일**: `03_FEATURE_INVENTORY.md` (섹션 2~3), `04_VISUAL_IDENTITY.md`

```
Yuminai의 핵심 차별 기능인 "Claude ⇄ Codex 통합" 가이드 챕터를 디자인해줘.

# 컨셉
같은 워크스페이스에서 두 AI agent (Anthropic Claude + OpenAI Codex)를 자유롭게 오가는 워크플로우.
- Claude (오렌지 #D97706) — 설계·리뷰
- Codex (틸그린 #10A37F) — 빠른 코드 생성

# 페이지 1 — 두 에이전트의 강점
- Claude vs Codex 비교 카드 2장 (각자 색상으로 강조)
- 모델 + 가격: Claude (Haiku/Sonnet/Opus, $0.80~$15.00/M), Codex (gpt-5-codex, o3, custom)
- "언제 어느 쪽?" 결정 가이드

# 페이지 2 — 통합 Picker
- Composer footer의 통합 picker UI 일러스트
- 메뉴 expanded view: Claude 섹션 + Codex 섹션
- 한 클릭에 agent + 모델 동시 변경 시퀀스
- per-agent settings 자동 격리 강조: "Claude (Opus/plan) → Codex → 다시 Claude → Opus/plan 복원"

# 페이지 3 — Quick Handoff
- assistant 메시지 + 하단 chip "↳ 이 답변을 Codex로 이어서 검토" 일러스트
- 클릭 → agent 전환 + 자동 prefix inject 시퀀스 (3 step)
- 시나리오 example (한국어):
  1) Claude (Opus, plan)으로 설계 작성
  2) chip 클릭 → Codex로 검토 요청
  3) Codex가 구현 → 다시 Claude로 돌아감

# 시각
- 좌측 strip 색상이 agent 인지의 핵심 — 강조해서 일러스트
- 핸드오프는 화살표 + 색상 그라디언트 transition으로 표현
- "오렌지 ⇄ 틸그린" 양방향 강조

산출물: HTML + CSS, 카드 형 레이아웃, 다크 default.
```

---

## 프롬프트 #5 — Telegram 통합 (모바일 ↔ 데스크톱)

> **사용 시점**: 모바일↔데스크톱 가이드 챕터
> **첨부 파일**: `02_PERSONA_AND_USE_CASES.md` (S2, S3), `03_FEATURE_INVENTORY.md` (섹션 5)

```
Yuminai의 "Telegram 모바일 ↔ 데스크톱" 가이드를 4 페이지로 디자인해줘.

# 컨셉
사용자가 책상을 떠나도 Telegram으로 진행 상황 받고, 외출 중에 명령 보낼 수 있는 워크플로우.
Multi-Bot 운영까지 포함 (여러 봇 → 여러 워크스페이스).

# 페이지 1 — 봇 셋업
- BotFather에서 봇 생성 → 토큰 입력 단계
- 첫 알림 테스트
- 사이드바 health pill 4가지 상태 (idle/healthy/degraded/failed) 시각

# 페이지 2 — 단방향 알림 + 응답 모드
- 작업 진행 중 Telegram 채팅 mockup (봇 → 사용자)
- 응답 모드 4단계 비교 카드:
  - minimal (~50 토큰) — ✓/✗ 한 줄
  - concise (~250) — 한 단락 + 다음 단계
  - standard (~800, default) — 결과 + 주요 변경
  - detailed (~3000) — 상세 reasoning
- 사용자 의사결정 inline keyboard example

# 페이지 3 — 양방향 명령 + Skills
- 모바일에서 메시지 → 데스크톱 자동 실행 시퀀스
- 사용자 정의 skills: /test, /review, /summary, /status
- /switch 명령으로 chat ↔ workspace 변경

# 페이지 4 — Multi-Bot 운영 (고급)
- 시나리오 A: 1 봇 × N 워크스페이스 다이어그램
- 시나리오 B: N 봇 × M 그룹 (팀별 격리) 다이어그램
- TelegramBotManagerSheet UI mockup (3 섹션: 봇 / 그룹 / Chat 매핑)

# 시각
- Telegram 채팅 mockup은 실제 텔레그램 모양 (둥근 말풍선, 인디고 accent)
- Health pill은 capsule 모양 with glow effect
- "외출 → 알림 → 답신" 시퀀스 다이어그램 (책상/지하철 아이콘 등)

산출물: HTML + CSS, 카드 형 레이아웃.
```

---

## 프롬프트 #6 — Workspace 정리 (핀, 폴더, Smart Folder)

> **사용 시점**: 멀티 프로젝트 운영 가이드 챕터
> **첨부 파일**: `03_FEATURE_INVENTORY.md` (섹션 1), `05_SCREEN_BY_SCREEN.md` (Sidebar)

```
Yuminai의 "워크스페이스 정리" 가이드 4 페이지를 디자인해줘.

# 컨셉
3~4개 프로젝트를 동시에 운영하는 솔로 개발자가 사이드바를 깔끔히 정리하는 방법.
Claude Code의 Pin + Codex CLI의 Folder 패턴 통합.

# 페이지 1 — 사이드바 구조 (개요)
- 사이드바 expanded screenshot (다크 모드, 한국어 UI)
- 위에서 아래로 라벨링: 핀 / Smart 그룹 / 폴더 / Uncategorized
- 좌측 2px accent bar = selected state

# 페이지 2 — 핀 + 폴더
- "워크스페이스를 폴더로 drag" 일러스트 (드래그 시퀀스)
- 폴더 색상 picker (10가지 색상)
- 폴더 아이콘 picker (SF Symbol)
- 핀: 자주 쓰는 워크스페이스 최상단 고정 + 순서 정렬

# 페이지 3 — Smart Folder + Tag
- Smart Folder 자동 그룹: "최근 7일", "텔레그램 연결됨"
- Tag system: 다중 태그 (urgent, client-X) + intersection 필터
- Smart Filter 저장 example
- ✨ wand 아이콘으로 Smart Folder 토글

# 페이지 4 — 빠른 전환 + 검색
- ⌘1 ~ ⌘9 키 캡 + 사이드바 1~9번 매핑 일러스트
- ⌘P Command Palette fuzzy search popover screenshot
- Import / Export (백업 archive)

# 시각
- 사이드바 component를 큰 일러스트로
- Drag & Drop은 화살표 + opacity transition
- 폴더 색상은 actual swatch로

산출물: HTML + CSS, 다크 default, 한국어.
```

---

## 프롬프트 #7 — 단축키 Cheat Sheet (1 페이지 reference)

> **사용 시점**: 단축키 reference 페이지
> **첨부 파일**: `06_KEYBOARD_SHORTCUTS.md`

```
Yuminai의 단축키 cheat sheet 1 페이지를 디자인해줘. 인쇄 가능한 reference 카드 스타일.

# 구조
4개 그룹을 2x2 grid로:
1. 글로벌 (⌘N, ⌘P, ⌘1-9, ⌘,, ⌘?, ⌘Q 등)
2. 채팅 (⌘↵, ⌘L, ⌘K, Esc, ⌘/, ⌘E, ⌘D 등)
3. 패널 (⌘⌥0/1/2/I/O 등)
4. 통합 (⌘⇧T, ⌘⇧M, ⌘⇧G, ⌘⇧B 등)

각 단축키:
[키 캡 그래픽] [동작 한국어 설명]

# 시각
- 키 캡은 실제 macOS 키처럼 (둥근 사각형, subtle border, monospace 글자)
- ⌘ 같은 modifier는 검은 배경에 흰 글자, 일반 키는 흰 배경에 검은 글자 (또는 다크 모드 inverse)
- 그룹 헤더는 brand color (보라/파랑) accent
- 페이지 상단에 워드마크 + "단축키 한눈에"

# 추가 요소
- 하단에 "💡 모든 sheet는 Esc로 닫을 수 있어요" tip
- A4 인쇄 가능 비율 (또는 1:1.414 ratio)

산출물: HTML + CSS (print-optimized), 또는 SVG. 다크 + 라이트 토글.
```

---

## 프롬프트 #8 — 메인 윈도우 일러스트 (히어로 보조)

> **사용 시점**: 가이드 표지 또는 챕터 헤더에 들어갈 앱 mockup 일러스트
> **첨부 파일**: `05_SCREEN_BY_SCREEN.md`

```
Yuminai 앱 메인 윈도우의 일러스트레이션을 그려줘. 가이드 표지/챕터 헤더에 사용.

# 구조 (다크 모드)
3-pane 레이아웃, 1440×900 비율:
- Sidebar (280pt, 좌): 핀 그룹 + 폴더 + 텔레그램 health pill 🟢
- Chat area (가변): PaneTabBar 상단 (Claude · Codex 탭) + 메시지 + Composer (좌측 오렌지 strip)
- Inspector (300pt, 우, 옵션): Obsidian 노트 트리

# 시각 디테일
- 배경: 메인 #1A1817 (warm dark), 사이드바 #161514, 카드 #211F1D
- Toolbar 상단: 워크스페이스 breadcrumb + 작은 아이콘 줄
- 메시지: User (cyan accent 박스, 우측) + Claude (라벨 + 본문, 좌측)
- 마지막 assistant 메시지 아래 hovering chip: "↳ 이 답변을 Codex로 이어서 검토"
- Composer 좌측 3px 오렌지 strip + footer 통합 picker (● Claude · Sonnet ⌄)

# 스타일
- 깔끔한 mockup illustration (실제 앱 같지만 완벽하지 않은 — 약간 stylized)
- 색상 토큰 정확히 사용
- 한국어 UI
- 가독성 우선 (디테일 일부 생략 OK)

# 옵션 variant
1. Full mockup (3-pane 모두)
2. Composer focus close-up (좌측 strip + 통합 picker 강조)
3. Sidebar focus close-up (핀 + 폴더 + health pill)

산출물: SVG (벡터, scalable), 또는 PNG @2x.
```

---

## 사용 팁 — 프롬프트 조합법

### "표지 + 1챕터" 빠른 시작
프롬프트 #2 (Welcome) + 프롬프트 #3 (Getting Started) 두 개로 사이트의 첫 인상 + 첫 챕터 완성.

### "핵심 차별 강조" 마케팅 페이지
프롬프트 #2 (Welcome) + 프롬프트 #4 (Claude⇄Codex) + 프롬프트 #5 (Telegram).
바이브 코더에게 가장 어필하는 3개 요소.

### "전체 풀 셋"
프롬프트 #1 한 번에 전체 또는, 페이지별로 나누어 #2 ~ #8 순차 적용.

### "디자인 일관성 체크"
모든 프롬프트에 공통:
- "04_VISUAL_IDENTITY.md의 색상 토큰 일관 적용"
- "다크 default, 한국어 UI"
- 위 문구를 프롬프트에 항상 포함시켜 일관성 유지.
