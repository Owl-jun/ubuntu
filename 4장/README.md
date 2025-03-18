## 시작과 종료

- X윈도우 기반의 리눅스라면 바탕화면에서 아이콘을 눌러 종료.
- 터미널에서는
```bash
poweroff
shutdown -P now
halt -p
init 0
```

- 유의해야할 것 : 대소문자구분 ,  일반사용자가 관리자 권한을 얻으려면 `sudo 명령어` 
- 프롬프트 구분 # : root , $ : user

- shutdown 명령어의 옵션

```bash
shutdown -P +10     # 10분 후 종료
shutdown -r 22:00   # 오후 10시에 재부팅
shutdown -c         # shutdown 예약 취소
shutdown -k +15     # 사용자에게 15분 후 종료된다는 메시지를 보내지만 , 실제로 종료되지는 않음
```

- 시스템 재부팅
```bash
reboot
shutdown -r now
init 6
```
- 로그아웃
```bash
logout
exit
```

- `Ctrl` + `Alt` + `F2` .... 현재 넘버의 가상콘솔로 이동

## 디렉터리

- 윈도우는 \로 디렉터리가 구분된다.
- 리눅스는 /로 구분된다.
- 윈도우는 C: D: 처럼 최상위 디렉토리가 여러개 있을 수 있지만, 리눅스는 / 하나뿐이다.
- 리눅스에서는 tree 라는 명령어가 디렉터리 구조를 알려준다.

```bash
tree / -L 4 | less # /부터 4단계 까지 출력해라, less 로 끊어서 출력 / 는 최상위 디렉토리이다.
Q # 실행종료

apt install tree # 트리가 동작하지 않을 시 설치

```

## 꼭 익혀두어야할 명령어들
- `man` 명령어 이름 으로 명령어 설명을 볼 수 있다

- `ls`
    - windows 의 dir 과 같은 녀석

```bash
ls                      # 현재 디렉터리의 목록
ls /etc/systemd         # 그냥 경로의 목록
ls -a                   # 목록 , 숨김파일포함(.으로시작하면 숨김파일처리)
ls -l                   # 자세히보기
ls *.conf               # 확장자 conf 찾기
ls -l /etc/systemd/n*   # n으로 시작하는놈들 찾기
```

- `cd`
    - 디렉토리 변경하는 녀석

```bash
cd                  # 사용자의 홈 디렉터리로 이동
cd ~ubuntu          # ubuntu 사용자의 홈 디렉터리로 이동
cd ..               # 부모 디렉터리로 이동
cd /etc/systemd     # 절대경로 이동
cd ../etc/systemd   # 상대경로로 이동
```

- `pwd`
    - Print Working Directory
    - 현재 작업중인 디렉터리 풀 경로 출력

- `touch` , `rm`
    - 크기가 0인 새 파일을 생성하거나 이미 파일이 존재한다면 파일의 최종수정 시간을 변경한다.
    - rm : 삭제명령어
```bash
touch abc.txt
rm abc.txt    # -f 와 매핑됨
rm -i abc.txt # 삭제 확인 문구나옴
rm -f abc.txt # 그냥 바로 삭제해버림
rm -rf abc    # abc 디렉터리와 그 아래에 있는 하위 디렉터리까지 모두 강제삭제 (편리하지만 매우 주의해서 사용해야함)
```

- `cp`
    - 파일 혹은 디렉터리를 복사, 복사한 파일은 사용자의 권한이 된다. 하지만 일기 권한이 있어야 실행가능하다.
```bash
cp abc.txt cba.txt  # abc -> cba 로 복사
cp -r abc cba       # 디렉터리 복사, abc 디렉터리를 cba 디렉터리로 복사
```

- `mv`
    - MoVe의 약자 디렉터리 이름변경 혹은 다른 디렉터리로 옮길 때 사용
```bash
mv abc.txt /etc/systemd/    # abc.txt 를 경로로 이동   
mv aaa bbb ccc ddd          # aaa, bbb, ccc 파일을 /ddd 디렉터리로 이동
mv abc.txt www.txt          # abc.txt 이름을 www.txt로 변경
```

- `mkdir` , `rmdir`
    - makedirectory의 약자로 새로운 디렉터리를 생성한다, 소유권은 생성한 유저에게 있다.
    - removedirectory 즉, 디렉터리를 삭제하는 명령어
```bash
mkdir abc           # 현재 디렉터리 아래에 /abc 디렉터리 생성
mkdir -p /def/fgh   # /def/fgh 디렉터리를 생성하는데 만약 /fgh 의 부모인 /def 가 없다면 자동 생성해줌. -p : Parents의 약자
rmdir abc           # abd 디렉터리 삭제
```

- `cat`
    - conCATenate의 약자로 파일 내용을 화면에 보여준다. 여러개 파일을 나열하면 파일을 연결해서 보여준다.
```bash
cat a.txt b.txt     # a.txt 와 b.txt 를 연결해서 파일의 내용을 화면에 보여줌
```

- `head` , `tail`
    - 텍스트 형식으로 작성된 파일의 앞 10행 또는 마지막 10행만 출력
```bash
head /etc/systemd/user.conf     # 앞 10행출력
head -3 /etc/systemd/user.conf  # 앞 3행출력
tail -5 /etc/systemd/user.conf  # 마지막 5행출력
```

- `more`
    - 텍스트 형식으로 작성된 파일을 페이지 단위로 화면에 출력한다. `Space Bar` 를 누르면 다음페이지로 이동, `B` 를 누르면 앞 페이지, `Q`를 누르면 종료
```bash
more /etc/systemd/system.conf
more +10 /etc/systemd/system.conf
```

- `less`
    - more과 유사하나, 화살표, `PageUp` , `PageDown` 키도 사용가능

```bash
less /etc/systemd/system.conf
less +10 /etc/systemd/system.conf
```

- `file`
    - 해당 파일이 어떤 종류의 파일인지 표시해준다.
```bash
file /etc/systemd/system.conf
file /bin/gzip
```

- `clear`
    - 화면 깨끗하게 지우기
```bash
clear
```


## 런 레벨
- init 뒤에 붙는 숫자를 런 레벨 이라고 부른다.
- 리눅스는 시스템이 가동되는 방법을 7가지 런레벨로 나눌 수 있다.

|런레벨 |영문 모드   |설명                        |비고          |
|:--:   |:--:       |:--:                       |:--:           |
|0      |Power Off  |종료 모드                   |              |
|1      |Rescue     |시스템 복구 모드            |단일 사용자 모드|
|2      |Multi-User |                           |사용하지 않음  |
|3      |Multi-User |텍스트 모드의 다중 사용자 모드|             |
|4      |Multi-User |                           |사용하지 않음  |
|5      |Graphical  |그래픽 모드의 다중 사용자 모드|             |
|6      |Reboot     |                           |              |

- 일반적으로 런레벨 3번을 Multi-User 모드로 사용한다. 2번과 4번은 우분투에서 사용하지 않지만 호환성을 위해 런레벨 3번과 동일하게 취급한다.

- 런레벨 확인하기
```bash
cd /lib/ststemd/system
ls -l runlevel?.target # ? 는 한 글자를 의미
# 현재 시스템 설정된 런레벨 : /lib/systemd/system/default.target 체크
```


- 런 레벨 실습

    - 시스템에 설정된 런 레벨 변경해보기

    1. 현재 설정된 런레벨 확인
        ```bash
        ls -l /lib/systemd/system/default.target
        systemctl get.default 
        ```
        
    2. 텍스트 모드로 부팅되도록 런 레벨변경해보기
        ```bash
        ln -sf /lib/systemd/system/multi-user.target /lib/systemd/system/default.target
        ls -l /lib/systemd/system/default.target

        systemctl set-default multi-user.target # 이 방법도 가능
        ```

    3. `Tab` 키 , 자동완성. 개꿀. 한/영 전환은 맥과 같이 `SHIFT`+`SPACE`
        - 화살표 위, 아래 키로 히스토리 체크가능
        ```bash

        history # 현재 명령어 히스토리 보여줌
        history -c # 히스토리 클리어
        ```


## 에디터 사용

- gedit 사용하기 (윈도우의 메모장 느낌)
    - 터미널
    ```bash
    gedit   

    # 실행 안될 시
    apt install gedit
    ```

- nano 에디터
    - 터미널
    ```bash
    nano

    ##### 적당히 내용입력후 `Ctrl` + `X`

    nano -c test.txt # 위치정보 자동으로 보여주는 방식으로 오픈
    ```    

- vi 에디터 (vim)
    - 실행
    ```bash
    cd /root
    vi
    ```
    - 종료
    
        - `ESC`
        ```bash
        :q
        ```
        - `ENTER`

    - `i` , `a` : 입력(insert) 혹은 추가(append)  
    - :wq : `ESC` 후 :wq 입력 시 저장 후 종료
    - 라인명령 모드 -> :i (취소) , :w (저장) , :q (종료)
    - :%s/q/qweqwe  -> q 를 모두 qweqwe 로 치환하라

- 마운트 , CD/DVD , USB의 활용

    ```bash
    mount //  마운트정보확인
    umount /dev/cdrom   // 기존마운트해제 , 오류나도 됨
    ```
    - /dev/cdrom == /dev/sr0 , 즉 CD/DVD 장치를 /dev/cdrom 으로 이해해도 무관

    - cp /boot/con* .    -> /boot/con~~파일을 현재 디렉터리(.) 에 복사


## 리눅스에서 ISO 파일 생성

```bash

apt -y install genisoimage
genisoimage -r -J -o boot.iso /boot
```