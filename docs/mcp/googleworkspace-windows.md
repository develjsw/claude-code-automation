# Google Workspace - gws CLI (windows)

## 도구 선택 기준

Google Workspace와 Claude Code 연동을 위한 도구로 **gws CLI**(`@googleworkspace/cli`)를 선택함
- gws CLI는 Google Workspace 공식 GitHub 조직(`github.com/googleworkspace/cli`)에서 관리하는 CLI 도구

| 옵션 | 상태                                 | 문제점 |
|------|------------------------------------|--------|
| Anthropic Google Drive MCP | 아카이브 (2024.11 이후 미업데이트)            | 읽기 전용, 드라이브만 지원, 더 이상 개발 안 됨 |
| 커뮤니티 Google Workspace MCP들 | 비공식                                | 유지보수 불안정, API 변경 대응 불확실 |
| **gws CLI** (`googleworkspace/cli`) | 공식 조직에서 개발시작 (2026.03~), 꾸준히 업데이트중 | - |

- google 공식 조직에서 개발중이며 꾸준하게 업데이트 되고 있기 때문에 gws cli를 선택함
- 아쉬운 부분은 3월부터 공개되어 공식 문서 외에는 자료를 찾기 힘들었고, 1건의 자료가 있었으나 mac 기준으로만 작성되어 있었음

---

### 1. gws CLI 설치
- 명령어 실행
  ```shell
  $ npm install -g @googleworkspace/cli
  ```
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp01.png" alt="gws CLI 설치 화면">

---

### 2. gcloud 설치
- gws는 내부적으로 gcloud를 사용하므로 설치 필수

<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp02.png" alt="gcloud 설치 화면 1">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp03.png" alt="gcloud 설치 화면 2">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp04.png" alt="gcloud 설치 화면 3">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp05.png" alt="gcloud 설치 화면 4">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp06.png" alt="gcloud 설치 화면 5">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp07.png" alt="gcloud 설치 화면 6">
- 아래 이미지처럼 한글 인코딩이 깨지는데 무시해도 됨
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp08.png" alt="한글 인코딩 깨짐 화면">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp09.png" alt="gcloud 설치 완료 화면">
- 위에 과정을 거치면 아래처럼 CMD창이 뜨는데 무시하고 끄기
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp10.png" alt="CMD창 화면">
- 설치 완료됐는지 확인
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp11.png" alt="gws 설치 확인 화면">

### 3. gws 권한 설정
- 아래 과정은 반드시 별도의 Powershell을 띄워서 진행 (webstorm과 같은 IDE에서 진행하면 UI가 잘리는 이슈 존재함)
- Step1. 명령어 실행
  ```shell
  $ gws auth setup
  ```
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp12.png" alt="gws auth setup 실행 화면">
- Step2. 로그인 및 인증<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp13.png" alt="로그인 화면 1">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp14.png" alt="로그인 화면 2">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp16.png" alt="로그인 화면 3">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp17.png" alt="인증 화면 1">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp18.png" alt="인증 화면 2">
- Step3. GCP Project 생성<br>
  - Create new project 커서 위치에서 Enter<br>
    <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp19.png" alt="GCP 프로젝트 생성 화면">
  - 프로젝트명 정하고 Enter (**전세계에서 고유한 값으로만 생성가능**)
    <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp20.png" alt="프로젝트명 입력 화면">
- Step4. 권한 허용할 API 리스트 설정
  - ↑↓키 이동하여 Space Bar로 선택 후 Enter
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp21.png" alt="API 리스트 설정 화면">
- Step5. Oauth 설정(테스트 사용자 생성, Oauth Client 생성 포함)
  - 아래 경로 복사 후 브라우저에 붙여넣기
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp22.png" alt="OAuth 설정 URL 화면">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp23.png" alt="OAuth 설정 화면 1"><br>
  - 값 작성<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp24.png" alt="OAuth 값 작성 화면 1">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp25.png" alt="OAuth 값 작성 화면 2">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp26.png" alt="OAuth 값 작성 화면 3">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp27.png" alt="OAuth 값 작성 화면 4">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp28.png" alt="OAuth 값 작성 화면 5"><br>
  - 테스트 사용자 생성<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp29.png" alt="테스트 사용자 생성 화면"><br>
  - Oauth Client 생성<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp30.png" alt="OAuth Client 생성 화면 1">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp31.png" alt="OAuth Client 생성 화면 2">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp32.png" alt="OAuth Client 생성 화면 3"><br>
  - 생성된 Oauth Client의 ID, 보안비밀번호 복사<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp33.png" alt="OAuth Client ID 복사 화면">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp34.png" alt="OAuth Client Secret 복사 화면"><br>
  - Oauth Client ID 입력 후 Enter<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp35.png" alt="OAuth Client ID 입력 화면"><br>
  - Oauth Client 보안비밀번호 입력 후 Enter<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp36.png" alt="OAuth Client Secret 입력 화면"><br>
  - 로그인 허용<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp37.png" alt="로그인 허용 화면"><br>
  - Enter<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp38.png" alt="Enter 입력 화면"><br>
  - 아래 경로 복사 후 브라우저에 붙여넣기<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp39.png" alt="재인증 URL 화면">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp40.png" alt="브라우저 인증 화면 1">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp41.png" alt="브라우저 인증 화면 2">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp42.png" alt="브라우저 인증 화면 3">
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp43.png" alt="브라우저 인증 화면 4"><br>
  - 다시 Powershell을 확인해보면 다음과 같이 success 되어 있음<br>
  <img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp44.png" alt="인증 success 화면">

### 4. Gws Skill 추가 (클로드 코드에서 gws 사용할 수 있도록 추가) 
- CLAUDE.md에 gws 사용 지시 추가
- `C:\Users\{username}\.claude\CLAUDE.md` 또는 프로젝트 CLAUDE.md에 아래 내용 추가

  ```markdown
  ## Google Workspace
  Google 관련 작업(메일, 드라이브, 캘린더, 스프레드시트, 문서 등)은 `gws` CLI를 사용해.

  - 기본 형식: `gws <service> <resource> <method> --params '{...}'`
  - 내장 워크플로우: `gws workflow +standup-report`, `+meeting-prep`, `+email-to-task` 등
  - Config 경로: `C:\Users\{username}\.config\gws\`
  ```

> Mac은 `/tmp/gws-cli/skills/`에 skills 파일이 추출되어 해당 경로를 참조했으나,
> Windows에서는 해당 폴더가 생성되지 않으므로 CLAUDE.md에 직접 명시하는 방식으로 대체

### 5. Test
- Gmail 조회 및 Drive 저장 요청
  ```shell
  claude$ 오늘 나에게 온 메일 최신 2개만 내 드라이브에 엑셀파일로 정리해서 생성해줘. 파일명은 20260413으로
  ```

<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp45.png" alt="gmail 및 drive 요청 화면">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp46.png" alt="gmail 조회 및 drive 저장 결과 화면 1">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp47.png" alt="gmail 조회 및 drive 저장 결과 화면 2">
<img width="600" src="../images/googleworkspace/windows/googleworkspace-mcp48.png" alt="gmail 조회 및 drive 저장 결과 화면 3">
