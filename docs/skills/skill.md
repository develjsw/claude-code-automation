# Claude Code Skill

### 1. 세 가지 방식 비교

| 방식     | 경로 | 형식 | 범위 | 상태 |
|--------|------|------|------|------|
| 전역 스킬 | `~/.claude/skills/<name>/SKILL.md` (Mac)<br>`%USERPROFILE%\.claude\skills\<name>\SKILL.md` (Windows) | 디렉토리 + SKILL.md | 모든 프로젝트 | 권장 |
| 프로젝트 스킬 | `<프로젝트>/.claude/skills/<name>/SKILL.md` (Mac, Windows) | 디렉토리 + SKILL.md | 해당 프로젝트만 | 권장 |
| 커맨드 (레거시) | `~/.claude/commands/<name>.md` (Mac)<br>`%USERPROFILE%\.claude\commands\<name>.md` (Windows) | 단일 .md 파일 | 전역/프로젝트 | 레거시 |

### 2. commands vs skills 차이

- **commands (레거시)**: 파일 하나가 곧 스킬
  ```
  EX)
  ~/.claude/commands/morning-briefing.md
  ```

- **skills (신규 권장 방식)**: 디렉토리 구조로 보조 파일 번들링 가능
  ```
  EX)
  ~/.claude/skills/morning-briefing/
  ├── SKILL.md     ← 메인 프롬프트 + 프론트매터
  └── (templates, scripts 등 보조 파일 가능)
  ```

- skills가 commands보다 추가로 지원하는 것:
  - 보조 파일 번들링 (템플릿, 스크립트 등)
  - `context: fork`로 격리된 서브에이전트 실행
  - `disable-model-invocation` / `user-invocable` 호출 제어
  - `allowed-tools`로 도구 자동 허용
  - `model` / `effort` 레벨 지정 (ex. `model: claude-opus-4-6`, `effort: low|medium|high|max`)
  - 같은 이름이면 skills가 commands보다 우선

### 3. SKILL.md 권장 형식

```markdown
EX)
---
name: morning-briefing
description: 오늘의 Gmail, Jira를 요약하여 Google Sheet 생성 후 Slack DM 발송
allowed-tools: "Bash mcp__atlassian__searchJiraIssuesUsingJql mcp__plugin_slack_slack__slack_send_message"
disable-model-invocation: true
argument-hint: "[날짜 (선택)]"
---

$ARGUMENTS 날짜 기준으로 다음을 수행해줘...
(프롬프트 본문)
```

### 4. 주요 프론트매터 필드

| 필드 | 설명 |
|------|------|
| `name` | 스킬명 (소문자, 하이픈). 생략 시 디렉토리명 사용 |
| `description` | 자동완성 목록에 표시 + Claude가 자동 호출 판단에 사용 |
| `allowed-tools` | 승인 팝업 없이 자동 허용할 도구 |
| `disable-model-invocation` | `true` 설정 시 사용자만 `/`로 호출 가능 (Claude가 자동 호출 안 함) |
| `user-invocable` | `false` 설정 시 Claude만 호출 가능 (메뉴에 안 보임) |
| `context: fork` | 격리된 서브에이전트에서 실행 |
| `argument-hint` | 자동완성 시 인자 힌트 표시 |
| `model` | 사용할 Claude 모델 지정 (ex. `claude-opus-4-6`) |
| `effort` | 응답 품질/속도 조절 (`low` \| `medium` \| `high` \| `max`) — `max`는 Opus 4.6 전용 |

### 5. 호출 방법

```shell
EX)
# 인자와 함께 호출
claude$ /morning-briefing 2026-04-12

# 인자 없이 호출 (argument-hint가 선택 사항인 경우)
claude$ /morning-briefing
```
