# 05 — 화면별 가이드 (Screen-by-Screen)

> 가이드의 스크린샷·일러스트·UI 설명에 활용. 각 영역의 *목적*과 *내용*만.

## 메인 윈도우 — 3-pane 레이아웃

```
┌────────────────────────────────────────────────────────────────────────┐
│  ⌘ Yuminai      Breadcrumb: nunchi/main · 5 commits ahead    ⓘ ⚙  ⚡   │ Toolbar (44pt)
├──────────┬────────────────────────────────────────────┬────────────────┤
│          │ ┌─────────── PaneTabBar ──────────────┐    │                │
│          │ │ ✨ Claude (설계) | <> Codex |  +     │    │                │
│ Sidebar  │ └──────────────────────────────────────┘    │  Inspector    │
│ (280pt)  │                                              │  (300pt)      │
│          │  ChatView                                    │               │
│ 📌 Pin   │  ┌─ User: "PRD대로 옵션 B 구현"          ┐  │  - Obsidian   │
│  nunchi  │  └────────────────────────────────────  ┘  │    노트 트리   │
│          │                                              │               │
│ 📁 Active│  ┌─ Claude: "Plan을 작성하겠습니다…"    ┐  │  - 슬래시     │
│  moodbit │  │  1. 인증 모듈 분리                     │  │    명령       │
│  emolab  │  │  2. ...                                │  │    카탈로그   │
│          │  └────────────────────────────────────  ┘  │               │
│ 🤖 Smart │     ↳ 이 답변을 Codex로 이어서 검토        │  - 통합 상태   │
│  Recent  │                                              │               │
│          │  ─────────────────────────────────────────   │               │
│ ────     │  ┌─ Composer (좌측 오렌지 strip = Claude)─┐  │               │
│ 🟢텔레그램│  │  > 메시지 입력 ...                      │  │               │
│  정상    │  │                                          │  │               │
│          │  │  ● Claude · Sonnet ⌄  default ⌄  med ⌄ │  │               │
│  yuminai │  └──────────────────────────────────────  ┘  │               │
│   ⚙      │                                              │               │
└──────────┴────────────────────────────────────────────┴────────────────┘
   280pt              가변(min 460pt)                     300pt
```

## 영역별 상세

### 1. Toolbar (상단, 44pt)
**목적**: 워크스페이스 컨텍스트 + 핵심 토글

- **앱 아이콘** (좌상)
- **Breadcrumb**: `워크스페이스명 / git branch · diff stats`
- **버튼 그룹** (반응형으로 일부 숨김):
  - 사이드바 토글 (`⌘⌥1`)
  - 검색 (`⌘P`)
  - Inspector 토글 (`⌘⌥2`)
  - Terminal 토글
  - Preview 토글
  - Commands 토글
  - Usage Dashboard
  - Shortcut Help (`⌘?`)
  - Settings (`⌘,`)

### 2. Sidebar (280pt, 좌측)
**목적**: 워크스페이스 정리 + 핀 + 폴더 + 텔레그램 health

#### 위에서 아래로 구조 (ADR-076)
1. **Top header**: collapse 버튼, 검색 버튼, Smart folders 토글 메뉴 (✨ wand)
2. **Tag filter chips** (탭이 있을 때만)
3. **📌 핀 그룹** (있을 때만, 항상 최상단) — drag reorder 가능
4. **🤖 Smart 그룹들** — 활성화된 자동 폴더 (recentWeek, telegramBound 등)
5. **📁 Folder 그룹들** — 사용자가 만든 폴더 (drop target, 색상/아이콘 customization)
6. **Uncategorized 그룹** — 폴더에 안 든 워크스페이스
7. **Update card** (필요 시)
8. **🟢/🟠/🔴 텔레그램 Health Pill** (ADR-086) — 활성 시만
9. **BottomUserCard** — 사용자 + 설정 아이콘

#### 워크스페이스 row
- 🟦 폴더 아이콘 (color customizable) | 워크스페이스 이름 | (옵션) git branch · 텔레그램 dot · drag handle
- selected = 좌측 2px accent bar

### 3. Chat Area (중앙, min 460pt)
**목적**: AI와 대화하는 메인 영역

#### 위에서 아래로 구조
1. **PaneTabBar** (28pt) — 탭 전환, `+` (Claude/Codex 추가), split mode picker, help hint
2. **ChildProcessBadge** (있을 때만) — 진행 중인 decomposition/rehearsal/parallel 표시
3. **ChatView** — 메시지 리스트 (scrollable, auto-scroll to bottom)
   - User message: 우측 accentMuted 박스 + 좌측 2px accent bar
   - Assistant message: 박스 없이, 라벨("Claude" / "Codex (설계)") + 본문
   - Tool message: 작은 dot + dimmed text
   - System message: 옅게 + center-aligned
   - **Handoff chip** (마지막 assistant 메시지 아래): `↳ 이 답변을 Codex로 이어서 검토`
4. **Composer** — 입력창 (104~320pt, agent strip)

### 4. Composer (입력창)
**목적**: 메시지 작성 + 모델 선택 + 첨부

```
┌─────────────────────────────────────────────────────────────┐
│ 📎 file1.swift  📎 file2.md            [모두 지우기]          │ Attachments (있을 때)
│ ───────────────────────────────────────────────────────────  │
│ ⎇ main · +24 -8                                              │ Git meta (있을 때)
│ ───────────────────────────────────────────────────────────  │
│ [좌측 3px 오렌지 strip = Claude / 틸그린 = Codex]            │
│ │                                                            │
│ │ 무엇을 도와드릴까요?                                         │
│ │ @codex / @claude 로 다른 pane에 위임                        │
│ │                                                            │
│ ┌────────────────────────── footer ──────────────────────┐  │
│ │ ● Claude · Sonnet ⌄  | default ⌄  |  medium ⌄  | 📎 📝 │  │
│ │                                              ▶ 전송 (⌘↵)│  │
│ └────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

#### Footer 요소 (왼쪽 → 오른쪽)
- **UnifiedAgentModelPicker** (가장 큰 버튼, agent + 모델)
- **Permission picker** (default / acceptEdits / auto / bypass / dontAsk / **plan**)
- **Effort picker** (low / medium / high / max) — `tiny` 모드에서는 숨김
- **첨부 (📎)** — 파일/폴더 picker
- **노트 첨부 (📝)** — Vault 설정 시만
- **Send/Stop** 버튼 (오른쪽 끝)
- **Streaming 인디케이터** ("응답 중" + pulse dot)

### 5. Inspector (300pt, 우측, 옵션)
**목적**: 보조 정보 (사용자 토글 가능, regular/wide mode에서만)

탭들:
- **Obsidian 노트 트리** (Vault 설정 시)
- **슬래시 명령 카탈로그**
- **통합 상태** (Telegram health, git status 요약)
- **Harness 탭** (옵션, ADR-049) — Conversation log + TaskGraph mini-map

---

## 주요 Sheet들 (모두 반응형, ADR-073/074)

### Settings (⌘,)
- 720×560 (ideal), 460×360 (min)
- 5~6개 탭: 일반 / 통합 / 외관 / 자동화 / 텔레그램 / 고급

### Create Workspace (⌘N)
- 워크스페이스 이름 + 디렉토리 picker + 하네스 템플릿 (empty/swift/typescript/python/general)
- (옵션) `git worktree add` 토글

### Command Palette (⌘P)
- fuzzy search input + 결과 리스트
- 워크스페이스 / 슬래시 명령 / 파일 / 노트 통합

### Shortcut Help (⌘?)
- 그룹별 단축키 cheat sheet (글로벌 / 채팅 / 패널 / Vault)

### Usage Dashboard
- **Compact view** (default): 오늘 비용 + 활성 시간 + 메시지 수
- **Detailed view**: 시계열 차트, agent×model 분포, forecast
- Agent/Model picker로 필터링

### Git Sheet들
- **Commit Sheet** — diff 미리보기 + AI 메시지 생성 버튼 + 메시지 편집
- **Branch Picker** — 브랜치 리스트 + 체크아웃/생성/삭제
- **Diff Viewer** — file별 diff
- **PR Sheet** — PR 생성/리뷰/머지 + GitHub Actions
- **Conflict Sheet** — conflict block 별 ours/theirs/both/custom
- **Stash Sheet** — save/pop/drop/apply
- **Rebase Sheet** — interactive rebase
- **Cherry-pick Sheet**

### Telegram Sheet들 (ADR-084 ~ 086)
- **TelegramAdvancedSheet** (⌘⇧T) — 응답 모드 / 토큰 budget / 첨부 / Skills / 연결+알림
- **TelegramBotManagerSheet** (⌘⇧M) — 봇 목록 / 그룹 / Chat ↔ Workspace 매핑
- **TelegramErrorLogSheet** — 카테고리 통계 + 최근 에러

### Folder Edit Sheet
- 폴더 이름 + 색상 (10가지) + 아이콘 (SF Symbol)

### Tag Edit Sheet
- 태그 이름 + 색상

### Note 관련
- **Create Note Sheet** — 새 노트 생성 (templates)
- **Wiki Disambiguation Sheet** — 같은 이름 노트 여러 개일 때

### About Sheet
- 앱 아이콘 + 버전 + 빌드 정보 + 라이센스

---

## 첫 실행 (Onboarding Wizard)

ADR-072 Phase 4 — 3-step wizard:

1. **Welcome** — Yuminai 1줄 설명, "시작" 버튼
2. **모드 선택**:
   - 🌱 **초보자** — 고급 옵션 숨김, 안전 기본값
   - 🚀 **고급** — 모든 옵션 노출
   - 🎨 **사용자 정의** — 항목별 토글
3. **Claude CLI 확인** — 자동 탐지 (`which claude`), 없으면 경로 입력
4. **(옵션) 통합 설정** — Obsidian Vault 경로, Telegram bot token (모두 skip 가능)

소요 시간: **5분 이내**

---

## 빈 상태 / 에러 상태

### 워크스페이스 없음 (첫 실행 후)
```
┌────────────────────────────────────────┐
│                                        │
│   Yuminai에 오신 것을 환영합니다         │
│                                        │
│   [+ 첫 워크스페이스 만들기]              │
│                                        │
│   또는 ⌘N                              │
│                                        │
└────────────────────────────────────────┘
```

### Claude CLI 없음
- 토스트: "Claude CLI를 찾을 수 없습니다. 설정에서 경로를 지정하세요."
- 버튼: [설정 열기]

### Claude CLI 비정상 종료
- 채팅 본문에 시스템 메시지: "Claude가 비정상 종료되었습니다 (exit 1). 다시 시도하시겠습니까?"
- 자동 재시작 안 함 (사용자 의사)

### 텔레그램 연결 실패
- 사이드바 health pill: 🔴 "실패" — 클릭으로 에러 상세
- Error log sheet: 카테고리별 통계 + 최근 에러 + 사용자 친화 한국어 메시지
