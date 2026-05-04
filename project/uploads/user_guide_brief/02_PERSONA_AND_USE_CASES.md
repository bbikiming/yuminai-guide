# 02 — 사용자 페르소나 & 핵심 시나리오

> 가이드의 청자(reader) · 예시 시나리오 · 페인포인트를 한 곳에.

## 주 페르소나 — "바이브 코더"

### 한 줄 묘사
> AI 페어 프로그래밍에 깊이 의존하는 솔로 풀스택 개발자.
> 여러 프로젝트를 동시 운영하며, Obsidian으로 사고하고 Telegram으로 모바일↔데스크톱을 잇는다.

### 프로필
- **역할**: 솔로 풀스택 개발자 + 디자인·기획 겸업
- **장비**: MacBook (Apple Silicon, macOS 26 Tahoe)
- **에디터**: Cursor / VS Code / Xcode 혼용 (Yuminai는 채팅 셸 — 코드 편집 X)
- **노트**: Obsidian Vault — 모든 기획·회고·메모가 모인 곳
- **소통**: Telegram을 봇 인터페이스로 적극 사용 (모바일↔책상)
- **이미 사용 중**: claude-forge 하네스, oh-my-claudecode, Plankton 등

### 운영 중인 프로젝트 (예시 이름)
- `nunchi` (눈치) — 메인 SaaS 프로덕트
- `moodbit` — 보조 프로덕트
- `emotion-lab` — 실험 프로젝트
- 디자인 시스템 — 공통 토큰

→ **3-4개 워크스페이스가 동시에 활성화됨** (가이드의 멀티 워크스페이스 예시로 활용)

## 페인포인트 (Yuminai가 풀어야 할 것)

### PP1. 컨텍스트 복붙 지옥 (가장 큼)
**현상**: Obsidian에 정리한 PRD/회고를 매번 직접 복사 → `claude` 입력창에 붙여넣기 → 결과는 다시 수동으로 노트에 옮김
**빈도**: 일 20~30회
**Yuminai 해결**: `@note-name` inline 삽입, 자동 노트화 (`/note save`), Daily Note 자동 append

### PP2. 세션 휘발
**현상**: 터미널 `claude` 종료/재부팅 시 대화 사라짐. 어제 어디까지 했는지 git log/노트 뒤져서 복원
**빈도**: 일 3~5회
**Yuminai 해결**: SwiftData 영속, 워크스페이스 재진입 시 자동 복원, 전체 텍스트 검색

### PP3. 자리 이탈 시 단절
**현상**: Claude가 30분 작업 중 외출 → 진행 모름. 막혔으면 그 시간 낭비
**빈도**: 주 5~10회
**Yuminai 해결**: Telegram 알림 (이정표/완료/에러), 모바일에서 추가 명령 가능 (양방향)

### PP4. 멀티 워크스페이스 병렬 운영
**현상**: 3~4개 프로젝트 동시 진행 — tmux/iterm 탭으로 분리하지만 컨텍스트 섞임
**빈도**: 일상
**Yuminai 해결**: 워크스페이스 = 사이드바 1급 시민, ⌘1~⌘9 빠른 전환, 폴더·핀·태그·smart filter

### PP5. 하네스 적용 마찰
**현상**: claude-forge의 rules/agents/skills를 프로젝트별로 다르게 적용하고 싶은데 `.claude/` 셋업이 매번 수동
**빈도**: 새 프로젝트마다
**Yuminai 해결**: 워크스페이스 생성 시 하네스 템플릿 (Swift/TypeScript/Python/General), `.harness/` 자동 스캐폴딩

## 핵심 시나리오 (가이드 예시로 활용)

### S1. 아침 루틴 (10분) — "오늘의 워크스페이스"
1. Yuminai 실행 → 사이드바 상단에 핀된 `nunchi` 클릭
2. 어제 마지막 세션 + Obsidian Daily Note 자동 컨텍스트 복원
3. 채팅에 `"오늘 할 것 목록 만들어줘"` → Claude가 Daily Note + 진행 중 PR 분석해서 답변
4. Composer 좌측 strip 색상으로 "지금 Claude 사용 중" 즉시 인지

> **가이드 활용**: "Getting Started" 챕터의 첫 5분 시나리오로

### S2. 깊은 작업 (1시간 자리 이탈) — "책상 떠나도 진행"
1. 큰 리팩토링 명령 입력 → Claude가 Plan 모드로 응답 → 사용자 승인 → 실행
2. 사용자: 점심 외출 (laptop 닫지 않음)
3. **Telegram 알림 도착**: "✅ 5/8 step 완료, 테스트 통과 중"
4. 외출에서 돌아옴 → "어디까지 했어?" → 진행 상황 + 남은 step 표시
5. 완료 시 Obsidian Daily Note에 작업 로그 자동 append

> **가이드 활용**: "Telegram 통합" 챕터의 메인 예시

### S3. 모바일 ↔ 데스크톱 (리모트 트리거)
1. 외출 중, Telegram 봇에 `"moodbit PR #42 머지하고 staging 배포 확인"` 메시지
2. 데스크톱 Yuminai가 알림 수신 → 워크스페이스 `moodbit` 자동 활성화
3. Claude에게 명령 전달 → 진행 상황 Telegram으로 1분마다 업데이트
4. 완료 시 결과 요약 + 만약 실패 시 inline keyboard로 의사결정 요청

> **가이드 활용**: "Multi-Bot 운영" 챕터 + "Quick Handoff" 데모

### S4. Claude ⇄ Codex 핸드오프 (ADR-087)
1. Claude (Opus, plan 모드)로 설계 작성
2. assistant 답변 받음 → 메시지 아래 `↳ 이 답변을 Codex로 이어서 검토` chip 클릭
3. **자동**: Codex로 agent 전환 + Composer에 "이전 설계 + 검토 요청" prefix
4. Codex (Sonnet)가 검토/구현
5. 다시 Claude로 돌아가도 last-used (Opus/plan) 자동 복원

> **가이드 활용**: "Multi-Agent 워크플로우" 챕터

## 사용하지 *않을* 시나리오 (가이드에서 빼야 할 것)

- 실시간 화상 회의 (Yuminai는 비동기 도구)
- 코드 직접 편집 (별도 에디터 담당 — Cursor/VS Code/Xcode)
- 디자인 작업 (Figma/Pencil 별도)
- 팀 협업 (1인용, 멀티유저 X)

## 안티 페르소나 (가이드의 청자가 *아닌* 사람)

| 안티 페르소나 | 왜 청자가 아닌가 |
|--------------|------------------|
| AI 코딩 신규 입문자 | Yuminai는 Claude Code 셋업/기본 개념을 가르치지 않음 — 프리퀴지트 |
| 팀 리드 | 협업 기능 없음 |
| 비개발자 (기획자/디자이너) | 코딩 워크플로우 위주, 불필요한 복잡성 |

→ 가이드는 "이미 Claude Code 또는 Codex CLI를 써본 경험이 있는 솔로 개발자"를 가정하고 작성.

## 핵심 메시지 우선순위 (가이드 첫 인상)

1. **"터미널 밖으로 꺼낸 Claude Code"** (가장 강한 차별점)
2. **"한 화면에 멀티 워크스페이스"** (Cursor/VS Code 채팅과 차별)
3. **"모바일에서 명령, 데스크톱에서 실행"** (유니크 가치)
4. **"Obsidian으로 사고, Yuminai로 실행, Daily Note로 정리"** (워크플로우 스토리)
