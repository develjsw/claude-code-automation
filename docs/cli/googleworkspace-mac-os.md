# Google Workspace - gws CLI (macOS)

> TODO : 추후 이미지와 함께 다시 정리예정
> Windows와 큰 차이점은 gcloud 설치 명령어, gws의 skills 경로, 설치 속도 뿐

---

### 1. 설치

```shell
$ brew install googleworkspace-cli
$ brew install --cask google-cloud-sdk
```

### 2. 권한 설정

```shell
$ gws auth setup
```

- Step1~2. 로그인 후 권한 허용
- Step3. 프로젝트명 생성 (**전세계에서 고유한 값으로만 생성가능**)
- 이후 과정은 Windows와 동일 (OAuth 설정, 테스트 사용자 생성 등)

### 3. Gws Skill 추가 (클로드 코드에서 gws 사용할 수 있도록 추가)

- Step1. gws 설치 시 자동 생성된 skills 폴더에서 원하는 스킬 확인
  ```shell
  $ cd /tmp/gws-cli/skills
  $ ls
  ```
  > Gmail, Drive, Calendar 등 서비스별 skill 파일(`.md`)이 존재
  > 필요한 스킬만 선택적으로 CLAUDE.md에 참조 가능

- Step2. 전역 경로의 CLAUDE.md에 gws 사용 지시 추가
  - `~/.claude/CLAUDE.md` 또는 프로젝트 CLAUDE.md에 아래 내용 추가

  ```markdown
  ## Google Workspace
  Google 관련 작업(메일, 드라이브, 캘린더, 스프레드시트, 문서 등)은 `gws` CLI를 사용해.

  - 기본 형식: `gws <service> <resource> <method> --params '{...}'`
  - Skills 참고: `/tmp/gws-cli/skills/`
  ```
