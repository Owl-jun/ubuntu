## 셸의 기본

- 셸은 입력한 명령을 해석해 커널로 전달 , 처리결과를 사용자에게 전달하는 역할
- 터미널과 비슷하다고 생각해도 무방하다.

### 우분투 bash 셸
- Alias 기능
- History
- 연산
- Job Control
- 자동 완성 `Tab`
- 프롬프트 제어 기능
- 명령 편집 기능

####  기본적인 사용법

```bash
(프롬프트) 명령 [옵션...] [인자...]
ls -l
rm -rf /mydir
find . / -name "*.conf"
```

#### 환경변수
- 셸은 여러 환경변수 값을 갖는다, 이를 확인하려면 `echo $환경변수이름` 을 활용하자.
```bash
echo $HOME : 현재 사용자의 홈 디렉터리
echo $LANG : 기본 지원되는 언어
echo $TERM : 로그인 터미널타입
echo $USER : 현재 사용자명
echo $COLUMNS : 현재 터미널의 컬럼 수
echo $PS1 : 1차 명령프롬프트 변수
echo $BASH : bash 셸의 경로
echo $HISTFILE : 히스토리 파일경로
echo $HOSTNAME : 호스트 이름
echo $LOGNAME : 로그인 이름
echo $MAIL : 메일을 보관하는 경로
echo $PATH : 실행파일 찾는 디렉터리 경로
echo $PWD : 사용자의 현재 작업 디렉터리
echo $SHELL : 로그인해서 사용하는 셸
echo $DISPLAY : X 디스플레이 이름
echo $LINES : 현재 터미널 라인 수
echo $PS2 : 2차 명령프롬프트 (대개는 '>')
echo $BASH_VERSION : bash 버전
echo $HISTSIZE : 히스토리 파일에 저장되는 개수
echo $USERNAME : 현재 사용자 이름
echo $LS_COLORS : ls 명령의 확장자 색상 옵션
echo $OSTYPE : 운영체제 타입

환경 변수 값을 변경하려면 export 환경변수=값
그 외 환경변수는 printenv 명령어 입력 시 출력됨
```

### 셸 스크립트 프로그래밍 실습
- C언어로 대부분 작성된 리눅스이기에, C언어와 유사하게 프로그래밍 가능하다.
