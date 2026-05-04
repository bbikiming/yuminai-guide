# 03 — 기능 인벤토리

> 87개 ADR로 구현된 모든 기능을 **9개 카테고리**로 그룹핑. 가이드 챕터 분할 기준.

## 한눈에 보기 — 9개 카테고리

| # | 카테고리 | 가이드 챕터 권장 | 핵심 ADR |
|---|---------|-----------------|---------|
| 1 | 워크스페이스 관리 | "프로젝트 정리" | 076·077·078·079 |
| 2 | 채팅 + Multi-pane | "AI와 대화하기" | 030·031·032·087 |
| 3 | Claude/Codex 통합 | "두 에이전트 함께 쓰기" | 026·087·088 |
| 4 | Obsidian 노트 통합 | "노트와 코드 연결하기" | 050 (S 시리즈) |
| 5 | Telegram 양방향 | "모바일에서 명령" | 058·084·085·086 |
| 6 | Git/GitHub 통합 | "버전 관리" | 081·082·083 |
| 7 | 사용량 대시보드 | "비용·생산성 트래킹" | 061·062·063·064·065·066·067·075 |
| 8 | 하네스/Multi-agent | "고급: 워크플로우 자동화" | 030·050·052·055 |
| 9 | 접근성 + 반응형 | (가이드 footer/메타) | 070·071·072·073·074 |

---

## 1. 워크스페이스 관리 (Workspaces)

### 핵심 개념
- **워크스페이스** = 보통 git 리포지토리 디렉토리에 1:1 대응하는 작업 단위
- 좌측 사이드바 1급 시민
- 각자 독립된 세션·메시지·하네스 컨텍스트 보유

### 기본 기능
- ✅ **CRUD**: 생성 (`⌘N`) / 이름 변경 / 삭제
- ✅ **빠른 전환**: `⌘1` ~ `⌘9` 워크스페이스 1~9번
- ✅ **검색**: `⌘P` (Command Palette / fuzzy search)

### 정리 도구 (ADR-076 ~ ADR-079)

| 기능 | 설명 |
|------|------|
| **핀 (Pin)** | 사이드바 최상단 고정. 자주 쓰는 워크스페이스 위로 |
| **폴더 (Folder)** | Codex CLI 스타일 그룹화. 색상·아이콘 사용자 변경 |
| **Smart Folder** | 자동 그룹 ("최근 7일", "텔레그램 연결됨", 등) |
| **태그 (Tag)** | 다중 태그 (`urgent`, `client-X`). 인터섹션 필터 |
| **Smart Filter** | 자주 쓰는 태그 조합을 저장 |
| **Drag & Drop** | 워크스페이스를 폴더로 드래그, 핀 순서 정렬 |
| **Import/Export** | 워크스페이스 메타 백업 (JSON archive) |
| **Duplicate** | 워크스페이스 복제 (디렉토리는 그대로) |
| **iCloud 동기화** | 메타데이터를 NSUbiquitousKeyValueStore로 동기화 |

### Project Profile
워크스페이스마다 **language / platform / backend / framework** 메타. Harness 자동 routing이 활용.

---

## 2. 채팅 + Multi-pane (Chat)

### 메인 채팅
- ✅ **메시지 스트리밍**: Claude/Codex CLI stdout을 실시간 렌더
- ✅ **Markdown 렌더링**: 코드블록 syntax highlighting (편집 X)
- ✅ **첨부**: 파일/폴더 → `@<path>` 자동 prepend
- ✅ **노트 첨부**: Obsidian 노트 → 본문 expand
- ✅ **Mention**: `@codex`, `@claude`로 다른 pane에 위임 (ADR-032)
- ✅ **Mention chain**: 응답에 `@<other>` 있으면 자동 dispatch (ADR-034)

### Composer (입력창) — ADR-087
- **좌측 3px agent 색상 strip**: Claude=오렌지, Codex=틸그린 (어느 agent로 보내는지 즉시 인지)
- **UnifiedAgentModelPicker**: 한 클릭에 agent + 모델 동시 선택 `[● Claude · Sonnet ⌄]`
- **Permission picker**: default / acceptEdits / auto / bypass / dontAsk / **plan**
- **Effort picker**: low / medium / high / max
- **Outer shadow agent tint** (focus 시 강조)

### Multi-pane (ADR-030)
한 워크스페이스 안에 N개 pane (각자 다른 agent + 세션):
- ✅ **PaneTabBar 상단**: 탭 전환, `+` 추가, `✕` 닫기
- ✅ **Split mode**: single / horizontal / vertical
- ✅ **Pane role**: primary (Telegram forward 대상) / secondary
- ✅ **이름 변경**: 더블클릭 (예: "Claude (설계)")

### Quick Handoff (ADR-087 Phase 4)
- 마지막 assistant 메시지 아래 chip: `↳ 이 답변을 Codex로 이어서 검토`
- 클릭 → agent 전환 + 이전 답변 + 검토 prefix 자동 inject

### 슬래시 명령
- `/help`, `/note save`, `/model`, `/test`, `/review`, `/summary`, `/status`, `/switch` (workspace) 등
- 자동완성, fuzzy search

---

## 3. Claude/Codex 통합 (Multi-Agent — ADR-087)

### Agent 종류
- **Claude** (오렌지 #D97706, "설계·리뷰에 강함")
  - 모델: Haiku / Sonnet / Opus (가격: $0.80/$3.00/$15.00 per M input)
- **Codex** (틸그린 #10A37F, "빠른 코드 생성")
  - 모델: OpenAI Codex CLI 자체 매핑 + 사용자 정의 (`~/.codex/config.toml`)

### Per-agent settings 격리 (ADR-087 Phase 1)
- 각 워크스페이스가 `[AgentKind: SessionSettings]` dict 보유
- agent 전환 → last-used model/permission/effort 자동 복원
- 예: Claude(Opus/plan) → Codex(Sonnet/default) → 다시 Claude(Opus/plan 복원)

### 통합 picker 메뉴 구조
```
🟠 Claude · 설계·리뷰에 강함
  ✓ Sonnet — 균형      $3.00/M in · $15.00/M out
    Haiku — 빠름·저비용  $0.80/M in · $4.00/M out
    Opus — 최고 성능    $15.00/M in · $75.00/M out
─────
🟢 Codex · 빠른 코드 생성
    gpt-5-codex
    o3
    사용자 정의 (~/.codex/config.toml)
```

---

## 4. Obsidian 통합

### 단방향 (컨텍스트 주입)
- ✅ Vault 경로 등록 → 노트 트리 사이드바
- ✅ 노트 클릭 → 채팅 입력창에 `@note-name` inline 삽입
- ✅ 전송 시 토큰이 본문으로 expand
- ✅ 검색 (Vault 전체 텍스트, fuzzy)

### 양방향 (자동 노트화)
- ✅ 작업 완료 시 Daily Note에 자동 append (옵션)
- ✅ `/note save` — 현재 세션 → 새 노트
- ✅ 템플릿 — 작업명, 시간, 핵심 변경, 후속

### Wiki link disambiguation
같은 이름 노트가 여러 폴더에 있을 때 sheet로 선택

---

## 5. Telegram 양방향 (ADR-058 ~ 067, 084 ~ 086)

### 알림 (단방향)
- 작업 시작/완료/실패 알림
- 사용자 의사결정 필요 시 inline keyboard
- 알림 종류 토글

### 양방향 명령 (ADR-058)
- 사용자가 Telegram에서 명령 → 데스크톱 Yuminai에 전달
- workspace binding (chat ID ↔ workspace)
- Plan-mode 강제 옵션 (ADR-046, 외부 turn 안전 기본값)

### 응답 모드 (ADR-084)
| 모드 | 토큰 | 설명 |
|------|------|------|
| **minimal** | ~50 | ✓/✗ 한 줄, 이동 중 가장 빠름 |
| **concise** | ~250 | 한 단락 요약 + 다음 단계 |
| **standard** | ~800 | (default) 결과 + 주요 변경/이유 |
| **detailed** | ~3000 | 상세 reasoning + diff 일부 |

### 토큰/비용 budget (ADR-084)
- per-turn max output / per-day max USD ($5 default) / per-chat daily max
- Overflow action: warn / block / downgrade (minimal로 강제 전환)

### 첨부 파일 (ADR-084)
- 사용자 → Yuminai (whitelist 확장자)
- Yuminai → 사용자 (자동 결과 파일 전송)

### Skills (ADR-084)
사용자 정의 prompt template:
- `/test` — 테스트 실행 (concise)
- `/review` — 코드 리뷰 (standard)
- `/summary` — 오늘 작업 요약 (concise)
- `/status` — 상태 확인 (minimal)

### 안정성 인프라 (ADR-085)
- **TelegramRetryPolicy**: exponential backoff + AWS full jitter
- **TelegramRateLimiter**: token bucket (30 msg/sec global, 1/sec/chat)
- **TelegramHealthMonitor**: AsyncStream으로 connection state observable
- **TelegramIdempotencyTracker**: update_id + message hash dedup
- **TelegramErrorClassifier**: auth / rateLimit / network / server / parsing / other

### Multi-bot (ADR-086)
3-tier hierarchy:
- **TelegramBotConfig** (개별 봇)
- **TelegramBotGroup** (그룹 — responseMode/budget override)
- **BotChatBinding** (chat × workspace 매핑)

→ 시나리오 A: 1봇 × N워크스페이스 / 시나리오 B: N봇 × M그룹

### Health UI (ADR-086 Phase 1)
사이드바 하단 connection pill:
- idle / healthy(green) / degraded(orange) / failed(red)
- 클릭 → Error log sheet

### Offline queue (ADR-086 Phase 2)
- Network 끊겼을 때 메시지 보관 → 복구 시 재전송
- drop-oldest, max=100, max attempts=5

### Webhook mode (ADR-086 Phase 5)
- LongPoll (default) / Webhook (HTTPS, 배터리 절약)

---

## 6. Git/GitHub 통합 (ADR-081 ~ 083)

### 기본
- ✅ 사이드바에 현재 브랜치/dirty stats 표시
- ✅ 워크스페이스 생성 시 `git worktree add` 옵션
- ✅ 브랜치 picker (popover)

### 커밋·푸시·풀 (ADR-081)
- ✅ **AI commit message 생성** (claude/codex가 diff 분석 → 메시지 작성)
- ✅ Commit sheet (메시지 편집 + 검토)
- ✅ Push / Pull
- ✅ Stash (save / pop / drop / apply)

### Branch 관리
- ✅ Branch picker
- ✅ Branch 생성/체크아웃/삭제
- ✅ Rebase (interactive)

### Conflict resolution (ADR-083)
- ✅ Conflict block parser
- ✅ "Accept ours / theirs / both / custom" UI
- ✅ Cherry-pick

### GitHub (gh CLI)
- ✅ PR 생성 / 머지
- ✅ PR comment 작성
- ✅ PR review
- ✅ Workflow re-run
- ✅ Repo insights
- ✅ Diff viewer

---

## 7. 사용량 대시보드 (ADR-061 ~ 067, 075)

### Compact view (default)
- 오늘 비용, 활성 시간, 메시지 수
- agent별 분포

### Detailed view ("자세히 보기")
- 시계열 차트 (SwiftUI Charts)
- agent × model × time 분포
- forecast (다음 7일 예상 비용)
- forecast accuracy 트래킹
- export (CSV / PNG / SVG)

### Telegram 사용량 dashboard (ADR-064)
- chat별 사용량
- 응답 모드별 토큰 분포
- 자동 알림 (사용량 80% 도달 시)

---

## 8. 하네스 + Multi-agent (Advanced)

### Harness 시스템
- `.harness/` 디렉토리 자동 스캐폴딩
- rules / agents / skills / hooks / commands 5개 디렉토리
- 워크스페이스별 + 글로벌 머지

### Harness 템플릿
신규 워크스페이스 시 선택:
- empty / swift / typescript / python / general

### Multi-agent 자동 routing (ADR-048)
- 사용자 입력 분석 → 적합한 agent로 자동 pane 전환
- handoff prompt 자동 inject
- 카운트다운 (3초 default, cancel 가능)

### Conversation log (ADR-050)
- 모든 turn이 conversation log에 기록
- 워크스페이스별 영속
- TaskGraph mini-map (Inspector)

### Routing decision log (ADR-052)
- 자동 routing 결정 사유 기록
- raw prompt 저장 토글 (privacy)
- 7일 retention

### Rehearsal (ADR-054)
- 작업 실행 전 plan만 미리 보기
- 사용자 승인 후 실제 실행

---

## 9. 접근성 + 반응형 (ADR-070 ~ 074)

### 반응형 (ADR-070, 072~074)
5단계 layout mode:
- **tiny** (< 600px) — 보조 모니터/split view
- **compact** (600~760) — sidebar overlay
- **medium** (760~1080) — sidebar inline, inspector hidden
- **regular** (1080~1440) — 표준
- **wide** (≥ 1440) — 모두 inline

Sheet도 모두 반응형 (`absoluteMinWidth=360`, `maxOfParentRatio=0.92`).

### 접근성 (ADR-071, 072)
- ✅ **WCAG 2.2 AA** 색 대비 (4.5:1) — Theme.Color 전체 audit
- ✅ **Focus indicator** 강화 (keyboard navigation visual)
- ✅ **VoiceOver labels** — 모든 인터랙티브 요소
- ✅ **macOS Voice Control** — 명령 매핑
- ✅ **초보자 모드** — 고급 옵션 숨기기 (default true 신규 사용자)
- ✅ **Onboarding wizard** — 초보자/고급/사용자 정의 선택 (3 step, 5분)

### 단축키 (ADR-074)
ShortcutHelpSheet에 전체 cheat sheet (`⌘?`).

---

## 카운트 요약

| 항목 | 수 |
|------|-----|
| 총 ADR | 87 (ADR-001 ~ ADR-087) |
| Phase 5 ADRs | 약 80% (각 ADR이 5 phase로 분해되어 구현) |
| 메인 sheet | 25+ |
| 메인 view | 14 |
| 단축키 | 30+ |
| 통합 외부 도구 | 5 (Claude CLI, Codex CLI, Obsidian, Telegram, Git/gh) |
| 단위 테스트 | 729 (모두 통과) |
