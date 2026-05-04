# 07 — 사용자 가이드 목차 (10챕터)

> 디자이너가 어떤 챕터를 만들어야 할지 결정하는 데 활용. 각 챕터에 들어갈 내용 + 추천 시각 요소.

## 추천 가이드 구조 — "10챕터 + 부록"

| # | 챕터 | 주제 | 길이 추정 | 페르소나 시나리오 |
|---|------|------|----------|-------------------|
| 0 | **Welcome** | 1줄 정의 + 비전 + 누구를 위한 도구인지 | 1 페이지 | — |
| 1 | **Getting Started** | 설치 → 첫 워크스페이스 → 첫 메시지 (5분) | 3 페이지 | S1 (아침 루틴) 일부 |
| 2 | **Workspaces** | 핀, 폴더, 태그, smart filter, 검색 | 4 페이지 | 멀티 워크스페이스 운영 |
| 3 | **AI와 대화하기** | 메시지 전송, 첨부, 슬래시 명령, mention | 4 페이지 | S1 (아침 루틴) 풀 |
| 4 | **Claude ⇄ Codex** | 두 에이전트 함께 쓰기, 핸드오프 | 3 페이지 | S4 (Claude/Codex) |
| 5 | **노트와 코드 연결** | Obsidian 통합, `@note`, daily note 자동 기록 | 3 페이지 | PP1 해결 |
| 6 | **모바일에서 명령** | Telegram 알림 + 양방향 + Multi-Bot | 4 페이지 | S2, S3 |
| 7 | **버전 관리** | Git: branch, commit, PR, conflict 해결 | 4 페이지 | "PR 만들고 머지" 시나리오 |
| 8 | **비용·생산성 트래킹** | Usage Dashboard, forecast | 2 페이지 | "한 달 비용 한눈에" |
| 9 | **고급: 워크플로우 자동화** | 하네스, multi-pane, plan mode, agent chain | 3 페이지 | 파워 유저 |
| 부록 A | **단축키 cheat sheet** | 전체 키보드 단축키 | 1~2 페이지 | reference |
| 부록 B | **트러블슈팅** | 자주 발생하는 문제 + 해결 | 2 페이지 | reference |
| 부록 C | **글로서리** | 도메인 용어 (워크스페이스, pane, harness 등) | 1 페이지 | reference |

**총 길이**: 약 **35~40 페이지** (밀도 높게) 또는 **70~80 카드** (각 페이지를 카드 2장씩)

---

## 챕터별 상세

### 0. Welcome (히어로)

**목적**: 첫 인상에서 "이 앱이 뭐고 누구를 위한 것인지" 5초 안에 전달.

**필수 요소**:
- 큰 앱 아이콘 (보라/파랑 그라디언트 Y)
- **Yuminai** 워드마크
- 1줄 정의 (`01_PRODUCT_BRIEF.md`의 1줄 정의)
- 슬로건 (예: "한 화면, 모든 코딩 사이클")
- "Get Started" CTA

**시각 요소 추천**:
- 메인 윈도우 mockup 스크린샷 (다크 모드)
- 워크플로우 다이어그램 (아침 → 작업 → 외출 → 완료) 한 줄

---

### 1. Getting Started (3 페이지)

**1.1 설치 + 첫 실행**
- macOS 26 요구사항 + Claude CLI 사전 셋업
- 첫 실행 시 Onboarding Wizard (3-step)
- 모드 선택: 초보자 / 고급 / 사용자 정의

**1.2 첫 워크스페이스**
- `⌘N` 또는 사이드바 `+`
- 디렉토리 picker (보통 git 리포지토리)
- 하네스 템플릿 선택 (empty / swift / typescript / python / general)

**1.3 첫 메시지**
- 채팅창 클릭 → 메시지 입력
- `⌘+Return` 전송
- Claude의 응답 스트리밍

**시각 요소**:
- Onboarding wizard 3-step screenshot
- 워크스페이스 생성 sheet
- 첫 응답 GIF (스트리밍 보여주기)

---

### 2. Workspaces (4 페이지) — "프로젝트 정리"

**2.1 사이드바 한눈에 보기**
- 핀 / 폴더 / Smart Folder / Uncategorized 구조
- 텔레그램 health pill (활성 시)

**2.2 핀과 폴더**
- 워크스페이스를 폴더로 drag → 그룹화
- 폴더 색상·아이콘 변경
- 핀: 자주 쓰는 워크스페이스 최상단 고정
- 핀 순서 drag 정렬

**2.3 Smart Folder & Tag**
- "최근 7일", "텔레그램 연결됨" 같은 자동 그룹
- 태그 시스템 — 다중 태그 + intersection 필터
- Smart Filter 저장

**2.4 빠른 전환 + 검색**
- `⌘1` ~ `⌘9` 빠른 전환
- `⌘P` Command Palette fuzzy search
- Import/Export (백업 archive)

**시각 요소**:
- 사이드바 expanded screenshot (핀 + 폴더 + smart 보임)
- 폴더 아이콘 색상 picker
- Drag & Drop 일러스트

---

### 3. AI와 대화하기 (4 페이지)

**3.1 Composer 한눈에**
- 메시지 입력 + 좌측 agent 색상 strip
- Footer 요소: agent picker / permission / effort / 첨부

**3.2 첨부와 컨텍스트 주입**
- 파일 드래그
- `@note-name`으로 Obsidian 노트
- `@<path>`로 파일 inline

**3.3 슬래시 명령**
- 자동완성 popover
- 글로벌 vs 워크스페이스 명령
- 즐겨찾기

**3.4 Multi-pane**
- 한 워크스페이스에 여러 pane (Claude + Codex)
- `@codex` mention으로 위임
- Split mode: single / horizontal / vertical
- Pane role: primary (Telegram forward) / secondary

**시각 요소**:
- Composer + 좌측 strip detail
- 슬래시 명령 popover
- Multi-pane split layout

---

### 4. Claude ⇄ Codex (3 페이지)

**4.1 두 에이전트의 강점**
- Claude (오렌지) — 설계·리뷰
- Codex (틸그린) — 빠른 코드 생성
- 가격 비교 (per M tokens)

**4.2 통합 Picker로 한 번에 전환**
- `[● Claude · Sonnet ⌄]` 큰 트리거
- 한 클릭에 agent + 모델 동시 선택
- per-agent settings 자동 격리 (last-used 복원)

**4.3 Quick Handoff (이어서 검토)**
- assistant 메시지 아래 chip
- "이 답변을 Codex로 이어서 검토" 클릭
- 자동 prefix + agent 전환

**시각 요소**:
- Picker 메뉴 expanded view
- Handoff chip 클릭 전후 비교
- per-agent settings flow 다이어그램

---

### 5. 노트와 코드 연결 (3 페이지)

**5.1 Obsidian Vault 등록**
- 설정에서 Vault 경로 입력
- 노트 트리 자동 빌드

**5.2 컨텍스트 주입**
- `@` 입력 → 노트 fuzzy search
- 선택 시 `@2026-05-01-DailyNote` 같은 토큰화
- 전송 시 본문 expand

**5.3 자동 노트화**
- `/note save` 슬래시 명령
- Daily Note에 자동 append (옵션)
- 작업 완료 시 템플릿 적용

**시각 요소**:
- Composer + `@` popover
- Daily Note에 append된 결과 example

---

### 6. 모바일에서 명령 (4 페이지)

**6.1 Telegram 봇 셋업**
- BotFather에서 봇 생성 → 토큰
- 설정에서 입력
- 첫 알림 테스트

**6.2 단방향 알림**
- 작업 시작/완료/실패
- 사용자 의사결정 inline keyboard
- 응답 모드 4단계 (minimal/concise/standard/detailed)

**6.3 양방향 명령**
- 모바일에서 메시지 → 데스크톱 실행
- `/test`, `/review`, `/summary`, `/status` skills
- `/switch <workspace>` chat-to-workspace 변경

**6.4 Multi-Bot 운영 (고급)**
- 여러 봇을 그룹으로 운영
- 시나리오 A: 1봇 × N워크스페이스
- 시나리오 B: N봇 × M그룹 (팀별 격리)

**시각 요소**:
- Telegram 채팅 mockup (봇 ↔ 사용자)
- Health pill 4가지 상태
- Multi-Bot 관리 sheet screenshot

---

### 7. 버전 관리 (4 페이지)

**7.1 Branch 관리**
- 사이드바 git 인디케이터
- `⌘⇧B` Branch picker
- Branch 생성/체크아웃/삭제

**7.2 AI Commit Message**
- `⌘⇧G` Commit Sheet
- "AI로 메시지 생성" 버튼 → diff 분석 → 메시지 작성
- 사용자 검토 + 편집 + commit

**7.3 PR 생성·머지**
- gh CLI 통합
- PR 생성 sheet → GitHub
- PR review (comment, request changes, approve)
- Workflow re-run

**7.4 Conflict 해결**
- Conflict block parser
- "Accept ours / theirs / both / custom"
- Cherry-pick + Rebase

**시각 요소**:
- Commit sheet AI 메시지 생성 시퀀스
- Conflict resolution UI
- PR 생성 → 머지 flow

---

### 8. 비용·생산성 트래킹 (2 페이지)

**8.1 Compact Dashboard (default)**
- 오늘 비용 / 활성 시간 / 메시지 수
- agent별 분포

**8.2 Detailed Dashboard ("자세히 보기")**
- 시계열 차트 (SwiftUI Charts)
- agent × model × time
- 7일 forecast + accuracy
- export (CSV / PNG / SVG)

**시각 요소**:
- Compact view + Detailed view 비교
- Forecast 차트 example

---

### 9. 고급: 워크플로우 자동화 (3 페이지)

**9.1 Plan Mode**
- 큰 task 시 plan mode → 사용자 승인 → 실행
- 외부 turn (Telegram) 시 자동 plan 강제 (안전 기본값)

**9.2 Harness 시스템**
- `.harness/` 자동 스캐폴딩
- rules / agents / skills / hooks / commands
- 글로벌 + 워크스페이스 머지

**9.3 Multi-Agent 자동 Routing**
- 사용자 입력 분석 → 적합한 agent로 자동 전환
- handoff prompt 자동 inject
- 카운트다운 (3초 default, cancel 가능)

**시각 요소**:
- Plan mode preview UI
- Harness 디렉토리 트리
- Routing decision log example

---

### 부록 A — 단축키 Cheat Sheet (1~2 페이지)

→ `06_KEYBOARD_SHORTCUTS.md` 그대로 사용

### 부록 B — 트러블슈팅 (2 페이지)

자주 발생하는 문제:
- "Claude CLI를 찾을 수 없음" → 경로 설정
- 텔레그램 health 빨간색 → Error log sheet
- Composer model picker가 안 바뀜 (이미 fix됨, ADR-087)
- 사이드바가 너무 좁아짐 → `⌘⌥1` 토글

### 부록 C — 글로서리 (1 페이지)

→ `09_GLOSSARY.md` 그대로 사용

---

## 가이드 디자인 권장 사항

### 레이아웃
- **다크 모드 우선** — 앱이 다크 default라 일관성
- **사이드 ToC** — 10챕터를 좌측에 항상 표시
- **카드 기반** — 각 페이지를 2~3장 카드로 (밀도 높지만 읽기 쉬움)
- **Inline 단축키** — `⌘N` 같은 표기는 monospace + subtle background

### 시각 패턴
- **챕터 헤더 색상**: 챕터별 brand gradient의 다른 stop 사용
  - Welcome: 보라 (#7C3AED)
  - Getting Started: 인디고 (#5B5DEF)
  - 후속: 파랑 (#3B82F6)
- **워크플로우 다이어그램**: 화살표 + 아이콘으로 단계 표현
- **스크린샷**: 다크 모드 / 한국어 UI / 실제 화면 vs mockup 둘 다 OK

### 인터랙티브 요소 (가이드가 웹이라면)
- 단축키 키 hover effect (실제 키처럼 누르는 애니메이션)
- 워크플로우 시퀀스 GIF/비디오
- "이 화면을 앱에서 열기" 딥링크 (Yuminai-specific URL scheme — 향후)
- TOC sticky + scroll spy
