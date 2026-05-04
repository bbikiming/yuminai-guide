# 09 — 도메인 용어집

> 가이드에서 일관된 용어를 쓰기 위한 reference. 각 용어는 한국어 + 영어 + 1줄 설명.

## A

### Agent (에이전트)
**한국어**: 에이전트
**의미**: Yuminai에서 사용하는 AI 코딩 도구. 현재 Claude (Anthropic)와 Codex (OpenAI) 2종.

### AgentKind
**의미**: enum — `claude` 또는 `codex`. 워크스페이스의 활성 에이전트를 표시.

### AgentPane
**의미**: 한 워크스페이스 안의 단일 에이전트 패널. 자체 세션·메시지·설정을 가짐. 한 워크스페이스에 N개 가능.

## B

### BotChatBinding (ADR-086)
**의미**: 텔레그램 봇 × chat × 워크스페이스 3-way 매핑. "이 chat은 어느 봇으로 들어와서 어느 워크스페이스로 라우팅되는지".

## C

### Claude Code
**의미**: Anthropic의 공식 코딩 CLI. Yuminai는 이를 자식 프로세스로 spawn해 사용 (A1 wrapper 패턴).

### Codex CLI
**의미**: OpenAI의 코딩 CLI. Yuminai의 두 번째 에이전트.

### Composer (입력창)
**의미**: 채팅 메시지를 작성하는 영역. 좌측 agent 색상 strip + footer (모델/모드/effort picker).

### Command Palette (⌘P)
**의미**: fuzzy search 인터페이스. 워크스페이스, 파일, 노트, 슬래시 명령을 한 곳에서 검색.

### Conversation Log (ADR-050)
**의미**: 모든 turn(사용자 입력 + agent 응답)이 기록된 single timeline. 워크스페이스별 영속.

## D

### Daily Note
**의미**: Obsidian에서 매일 자동 생성되는 노트. Yuminai가 작업 결과를 자동으로 append할 수 있음.

### Deferred (배포)
**의미**: 작업이 완료되었지만 아직 머지 전 상태. ADR-058 audit deferred 워크플로우 참조.

## E

### Effort Level
**의미**: 추론 강도. `low / medium / high / max`. 모델별로 작업 깊이를 조정.

## H

### Handoff (핸드오프)
**의미**: 한 agent의 답변을 다른 agent에게 검토 요청 — Composer chip 클릭으로 한 번에 (ADR-087 Phase 4).

### Harness (하네스)
**의미**: claude-forge 패턴 — `.harness/` 디렉토리에 rules / agents / skills / hooks / commands 파일을 워크스페이스별로 끼워넣어 워크플로우 자동화.

### Health Pill (ADR-086)
**의미**: 사이드바 하단 텔레그램 connection status 인디케이터. idle / healthy / degraded / failed 4가지 상태.

## I

### Inspector
**의미**: 우측 보조 패널 (300pt). Obsidian 노트 트리 + 슬래시 명령 카탈로그 + 통합 상태. `⌘⌥2`로 토글.

### Idempotency Tracker (ADR-085)
**의미**: 같은 메시지를 두 번 받았을 때 중복 처리 방지. update_id + message hash dedup.

## K

### Keychain
**의미**: macOS 시스템 시크릿 저장소. Yuminai의 모든 토큰 (Anthropic API, Telegram bot)이 여기 저장.

## L

### Layout Mode (ADR-070)
**의미**: 윈도우 너비에 따른 5단계 레이아웃 — `tiny` (< 600) / `compact` / `medium` / `regular` / `wide` (≥ 1440).

### Liquid Glass
**의미**: macOS 26 신규 디자인 언어. Yuminai는 사이드바·툴바·패널 분할에만 적용 (chrome only).

## M

### Mention (멘션)
**의미**: `@codex`, `@claude`처럼 다른 pane을 호출. ADR-032에 정의.

### Multi-pane (ADR-030)
**의미**: 한 워크스페이스에 여러 agent pane을 동시 띄우기. 같은 디렉토리 공유 → file system이 협업 매개체.

## O

### Onboarding Wizard (ADR-072)
**의미**: 첫 실행 시 3-step 마법사. Welcome → 모드 선택 (초보자/고급/사용자 정의) → CLI 확인.

### Obsidian Vault
**의미**: 사용자의 노트 보관소 (디렉토리). Yuminai가 노트를 컨텍스트로 주입하거나 자동 노트화에 사용.

## P

### Pane Role (ADR-030)
**의미**: pane의 역할 — `primary` (Telegram forward 대상, 1개) / `secondary` (보조).

### Per-Agent Settings (ADR-087)
**의미**: 각 워크스페이스가 agent별로 다른 model/mode/effort를 기억. agent 전환 시 자동 swap.

### Permission Mode
**의미**: Claude/Codex CLI에 전달되는 `--permission-mode` 값. `default / acceptEdits / auto / bypassPermissions / dontAsk / plan`.

### Pin (핀)
**의미**: 사이드바 최상단에 고정한 워크스페이스. 자주 쓰는 것 강조.

### Plan Mode
**의미**: Claude/Codex의 권한 모드 중 하나. 코드 실행 없이 계획만 작성. 외부 turn (Telegram) 시 안전 기본값으로 자동 강제.

## R

### Rate Limiter (ADR-085)
**의미**: 텔레그램 API 보호용 token bucket. 30 msg/sec global, 1 msg/sec/chat.

### Rate Limit Alert (ADR-086 Phase 2)
**의미**: 일별 budget의 80% 도달 시 텔레그램으로 자동 경고 + cooldown.

### Response Mode (ADR-084)
**의미**: 텔레그램 응답의 detail level — `minimal / concise / standard / detailed`.

### Retry Policy (ADR-085)
**의미**: 네트워크 실패 시 exponential backoff + AWS full jitter로 재시도.

### Routing Decision Log (ADR-052)
**의미**: 자동 routing 결정 사유 기록. raw prompt 저장 토글 (privacy), 7일 retention.

## S

### Session
**의미**: 워크스페이스 안의 한 conversation. SwiftData에 영속.

### Sidebar
**의미**: 좌측 워크스페이스 리스트 패널 (280pt). 핀 / Smart Folder / 폴더 / Uncategorized / Health pill / User card.

### Skills (Telegram, ADR-084)
**의미**: 사용자 정의 prompt template — `/test`, `/review`, `/summary`, `/status` 등. `{args}` 자리표시자 지원.

### Smart Filter (ADR-079)
**의미**: 자주 쓰는 태그 조합을 저장한 필터 preset.

### Smart Folder (ADR-077)
**의미**: 자동 그룹 — "최근 7일", "텔레그램 연결됨" 등.

### Streaming (스트리밍)
**의미**: Claude/Codex CLI의 stdout을 실시간 UI에 렌더. live dot pulse로 표시.

## T

### Tag (태그) (ADR-078)
**의미**: 워크스페이스에 붙이는 다중 라벨. intersection 필터 (모든 태그 만족).

### TaskGraph (ADR-049)
**의미**: Harness conversation의 task 의존성 그래프. Inspector mini-map에 표시.

## U

### UnifiedAgentModelPicker (ADR-087 Phase 2)
**의미**: Composer footer의 큰 트리거. 한 클릭에 agent + 모델 동시 선택.

## V

### Vault
**의미**: → Obsidian Vault 참조.

## W

### Workspace (워크스페이스)
**의미**: Yuminai의 작업 단위. 보통 git 리포지토리 디렉토리에 1:1 대응. 사이드바 1급 시민.

### Workspace Folder (ADR-076)
**의미**: 사이드바에서 워크스페이스를 그룹핑하는 사용자 정의 폴더. 색상·아이콘 customization.

## 약어

| 약어 | 풀이름 | 한국어 |
|------|--------|--------|
| ADR | Architecture Decision Record | 의사결정 기록 |
| API | Application Programming Interface | API |
| CLI | Command-Line Interface | 명령줄 도구 |
| CRUD | Create / Read / Update / Delete | CRUD |
| DM | Direct Message | 다이렉트 메시지 |
| LLM | Large Language Model | 대형 언어 모델 |
| MVP | Minimum Viable Product | 최소 기능 제품 |
| PR | Pull Request | PR / 풀 리퀘스트 |
| PRD | Product Requirements Document | 제품 요구사항 문서 |
| SPM | Swift Package Manager | Swift 패키지 매니저 |
| SwiftUI | (no expansion) | SwiftUI |
| UX | User Experience | 사용자 경험 |
| WCAG | Web Content Accessibility Guidelines | 웹 접근성 가이드라인 |

## 한국어 표기 권장 (가이드 일관성)

| 영어 | 한국어 (가이드 권장) |
|------|---------------------|
| Workspace | 워크스페이스 ('작업공간' X) |
| Pane | pane (그대로) 또는 패널 |
| Sheet | sheet (그대로) 또는 시트 |
| Picker | picker (그대로) 또는 선택기 |
| Branch | branch / 브랜치 |
| Commit | commit / 커밋 |
| Pull Request | PR / 풀 리퀘스트 |
| Merge | 머지 (병합 X — 사용자 본인 단어) |
| Onboarding | 온보딩 |
| Settings | 설정 |
| Agent | 에이전트 (선택적, 영문 그대로도 OK) |
| Inspector | Inspector (그대로 — 한국어 직역 어색) |
| Sidebar | 사이드바 |
| Toolbar | 툴바 |
