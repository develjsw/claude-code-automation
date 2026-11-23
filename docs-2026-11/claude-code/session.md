# Claude Code 세션 관리

> **작성일** : 2026-11-20

> **확인 버전** : Claude Code 2.1.311 / 공식 문서 2026-11-23 수정본 기준

> **주의** : 세션명(직접 지정·자동 생성·변경 모두)에 공백이 있으면 셸 명령어(`claude -n`, `claude -r`)에서 `"`로 감싸서 실행
> ```shell
> EX)
> $ claude -r 현재 프로젝트 작업 현황     (X)
> $ claude -r "현재 프로젝트 작업 현황"   (O)
> ```

---

### 1. 세션 시작

| 목적 | 명령어 | 설명 |
|------|--------|------|
| 세션명을 정해서 시작 | `claude -n 세션명` | `--name`과 동일, `/resume` 선택 화면과 터미널 제목에 표시 |
| 단발성 실행 | `claude -p "질문"` | 대화형 화면 없이 응답 출력 후 종료, 기본으로 디스크에 저장 |
| 저장 없이 단발성 실행 | `claude -p "질문" --no-session-persistence` | 디스크에 저장하지 않아 재개 불가, `-p`에서만 사용 가능 |

- 예시
  ```shell
  $ claude -n session-docs
  ```

### 2. 세션명 변경

| 목적 | 명령어 | 설명 |
|------|--------|------|
| 시작 후 이름 변경 | `/rename 세션명` | 세션 안에서 입력, 프롬프트 바에도 세션명 표시 |

- 예시
  ```shell
  claude$ /rename session-docs
  ```
- 세션명 미지정 시: 첫 프롬프트를 요약한 제목이 자동 생성되며, 이 제목으로도 `claude -r` 재개 가능

### 3. 세션 재개

| 목적 | 명령어 | 설명 |
|------|--------|------|
| 세션명으로 재개 | `claude -r 세션명` | 현재 저장소 안에서 검색 |
| UUID로 재개 | `claude -r 세션UUID` | 다른 프로젝트의 세션까지 검색, 어느 디렉터리에서든 실행 가능 |
| 선택 화면 열기 | `claude -r` (세션 밖)<br>`/resume` (세션 안) | 세션 목록 화면 진입, 기본으로 현재 디렉터리의 세션 표시 |
| 최근 세션 이어가기 | `claude -c` | 현재 디렉터리의 가장 최근 세션 재개 |

- `--resume`은 `-r`, `--continue`는 `-c`와 동일
- 선택 화면 단축키: `claude -r` 또는 `/resume`으로 세션 목록 화면에 진입한 뒤 사용

  | 단축키 | 설명 |
  |--------|------|
  | `Ctrl+A` | 모든 프로젝트의 세션까지 표시, 다시 누르면 현재 저장소로 복귀 |
  | `Ctrl+R` | 세션명 변경 |

- 다른 프로젝트의 세션 선택 시: 바로 열리지 않고 `cd` + 재개 명령어가 클립보드에 복사됨 (해당 프로젝트 디렉터리가 남아 있는 경우)
- `claude -p`로 만든 세션: 선택 화면과 `claude -c`에 미표시, `claude -r 세션UUID`로 재개 가능
- 다른 디렉터리에서 `claude -p -r 세션UUID`로 재개 시: 대화는 원래 세션에 이어서 기록, 작업 디렉터리는 명령어를 실행한 디렉터리 (직접 실행으로 확인, 대화형 세션은 미확인)

### 4. 저장 위치

- 기준 경로: `~/.claude/` (Mac), `%USERPROFILE%\.claude\` (Windows)

| 내용 | 경로 | 자동 삭제 |
|------|------|-----------|
| 대화 본문 | `projects/<경로>/<세션UUID>.jsonl` | O |
| 자동 메모리 | `projects/<경로>/memory/` | X |
| 입력 기록 | `history.jsonl` | X |

- `<경로>` 규칙: 작업 디렉터리 경로에서 영문자·숫자가 아닌 문자를 모두 `-`로 변환
  ```
  EX)
  /Users/sangwoo/projects/develjsw-repo/claude-code-automation
  → -Users-sangwoo-projects-develjsw-repo-claude-code-automation
  ```

### 5. 자동 삭제

| 항목 | 내용 |
|------|------|
| 설정 키 | `cleanupPeriodDays` (ex. `~/.claude/settings.json`) |
| 기본값 | 30일 (최솟값 1) |
| 삭제 대상 | 기간이 지난 대화 본문 등 세션 데이터 (자동 메모리, 입력 기록은 유지) |
| 삭제 시점 | 세션 시작 후 백그라운드에서 실행, 삭제 시 별도 메시지 없음 |
| 삭제 결과 | 삭제된 세션은 선택 화면에서 사라지며 재개 불가 |
| 기간 늘리기 | 큰 값 지정 (ex. `3650`), `0`은 검증 오류로 사용 불가 |
| 수동 삭제 | `claude purge <프로젝트 경로>` (`--dry-run`으로 삭제 대상 미리 확인) |

- 설정 예시
  ```json
  {
    "cleanupPeriodDays": 3650
  }
  ```

### 참고 문서

- [sessions](https://code.claude.com/docs/en/sessions)
- [cli-reference](https://code.claude.com/docs/en/cli-reference)
- [claude-directory](https://code.claude.com/docs/en/claude-directory)
- [settings-reference](https://code.claude.com/docs/en/settings-reference#cleanupperioddays)
