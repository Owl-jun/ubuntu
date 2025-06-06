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

# 사용자와 그룹관련 명령어

1. adduser
```bash
adduser newuser1            # newuser1 이라는 이름의 사용자생성
    신규 비밀번호 :          # 암호 생성
    신규 비밀번호 재입력 :   
    이름 [ ] :              # 여기서부터 생략가능 
    방 번호 [ ]
    직장 전화번호 [ ]
    집 전화번호 [ ]
    기타 [ ]
    정보가 올바릅니까? [Y/n]

adduser -uid 1111 newuser2  # newuser2 생성 , 사용자 ID 1111

adduser -gid 1000 newuser3  # newuser3 생성 , 그룹 ID 1000번에 포함시킴


adduser -home /newhome newuser4 # 생성과 동시에 홈 디렉터리를 /newhome 으로지정

adduser -shell /bin/sch newuser5 # 생성과 동시에 기본 셸을 /bin/sch로 지정
```
    
보통 암호는 8글자 이상 사전에 없는 단어로 지정하자.

2. passwd
    
    일반 사용자 : 본인의 비번만 지정/변경
    root 사용자 : passwd 사용자이름 명령으로 모든사용자 관리 가능

```bash
passwd newuser1     # newuser1 비번지정 (root 로그인시)
```

3. usermod

    사용자의 속성을 변경한다.
```bash
usermod --shell /bin/sch newuser1   # 기본셸변경
usermod --groups ubuntu newuser1    # 사용자 보조그룹에 ubuntu 그룹 추가
```

4. userdel
    사용자를 삭제한다.
```bash
userdel newuser2    # 삭제한다. 단, 홈 디렉터리는 삭제안됨
userder -r newuser3 # 홈 디렉터리까지 삭제
```

5. chage(CHange AGE)
    
    암호를 주기적으로 변경하도록 설정
```bash
chage -l newuser1   # 해당 ID에 설정된 사항 확인
chage -m 2 newuser1 # 한번 설정 후 최소사용일자, (여기선 최소 2일은 사용해야함)

chage -M 30 newuser1 # 이 암호를 사용할 수 있는 최대일자. (30일 후 변경해야됨)

chage -E 2030/12/12 newuser1 # 암호 만료날짜 (2030/12/12 만료)

chage -W 10 newuser1    # 암호 만료 전 경고날짜, 기본값 7일
```

6. groups

    사용자 소속 그룹표시
```bash
groups  # 현재 사용자 소속그룹 보여줌
groups newuser1 # 해당 사용자 그룹보여줌
```

7. groupadd

    새로운 그룹 생성
```bash
groupadd newgroup1
groupadd --gid 2222 newgroup2   # 그룹id 2222 인 그룹생성
```

8. groupmod

    그룹 속성 변경
```bash
groupmod --new-name mygroup1 newgroup1  # 그룹이름 my -> new로 변경
```

9. groupdel

    그룹 삭제
```bash
groupdel newgroup2 # 해당 그룹을 주요그룹으로 지정한 사용자가 없다면 그룹삭제
```

10. gpasswd

    그룹 비번 설정 혹은 그룹관리 수행
```bash
gpasswd mygroup1                # 그룹 암호지정
gpasswd -A newuser1 mygroup1    # user를 그룹의 관리자로 지정
gpasswd -a newuser4 mygroup1    # user를 그룹의 사용자로 추가
gpasswd -d newuser4 mygroup1    # user를 그룹에서 제거
```


# 허가권, 소유권

- 3bit씩 3칸이 존재.

|-|User|-|-|Group|-|-|Other|- |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|r|w|-|r|-|-|r|-|-|
|4|2|0|4|0|0|4|0|0|

- setuid , setgid , sticky
    - root , group 등의 허가권을 잠시 빌려주겠다.
    - rw`s`r-xr-- : 4754 (맨 앞 4가 setuid를 뜻함)
    - rwxr-`s`r-- : 2754 (맨 앞 2이 setgid를 뜻함)
    - rwxr--r-t   : 1745 (맨 앞 1이 sticky를 뜻함)
    - 대문자 S, T 가 위치할 경우는 실행권한이 없음을 뜻함, 숫자는 동일

- 3bit 씩 끊어읽자, 만약 허가권이 754 -> rwx r-x r-- 라는 뜻
- 허가권 변경 명령어 `chmod`
```bash
chmod 777 sample.txt
ls -l sample.txt

chmod u+wx sample.txt # User 에게 w x 기능 허가하라
chmod u-r sample.txt  # User 에게 r 기능 삭제하라
```

- 소유권
```bash
chown user1 sample.txt
chown user1:ubuntuGroup sample.txt
chgrp ubuntu sample.txt
```

- 심볼릭 링크과 하드링크
    - 하드링크 : 원본 그 자체 CPP의 레퍼런스와 비슷한 개념으로 이해
    - 심볼릭링크 : 윈도우의 바로가기 시스템, 원본 파일이 이동되면 연결이 끊어짐


- dpkg
    - 데비안 리눅스에서 설치 후 바로 실행할 수 있는 설치파일 제공, *.deb (패키지)
    ```bash
    dpkg -i 이름.deb    #설치
    dpkg -r             #삭제
    dpkg -P 이름        #삭제 및 설정파일까지 제거
    dpkg -l 이름        #패키지 정보 보여줌
    dpkg -L 이름        #패키지가 설치한 파일 목록 보여줌
    pkg --info 패키지파일이름.deb   # 패키지 파일 정보
    ```

    - dpkg 의 단점 : 의존성
    - 어떤 deb 파일을 설치할 때 다른 패키지가 필요하다면, 의존성 문제로 다운이 되지않는 경우가 있는데, 이를 간편하게 해결하고자 나온 것이 `apt` 이다

    - `apt`

    ```bash
    apt -y install 패키지이름   # -y : yesno 자동yes처리
    apt update                 # etc/apt/sources.list 파일 업데이트

    apt remove 패키지이름
    apt purge 패키지이름
    apt autoremove

    apt clean   # 내려받은 파일 제거
    apt autoclean

    apt-cache show 패키지이름       #패키지정보
    apt-cache depends 패키지이름    #의존성정보
    apt-cache rdepends 패키지이름   #역의존성정보
    ```

    - 파일압축

    `xz`
    ```bash
    xz 파일명  # 기존파일 삭제 후 압축파일 파일명.xz 생성
    xz -d 파일이름.xz   # decomp 압축풀기
    xz -l 파일이름.xz   # 압출 파일의 목록 및 압축률    list
    xz -k 파일이름      # 압축 후 기존 파일 삭제하지않음 keep
    ```
    `bzip2`
    ```bash
    bzip2 파일이름  # 압축
    bzip2 -d 파일이름.bz2   # 압축풀기
    bzip2 -k 파일이름 # keep
    ```
    `zip/unzip` : window 호환
    ```
    zip name.zip
    unzip name.zip
    ```

    - 원래 압축은 파일 압축 -> 압축된 파일 묶기 순서이다.

    - 파일 묶기
    `tar`
    ``` bash
    c -> 묶음생성
    x -> 묶인 파일 풀기
    t -> 묶음 풀기 전 묶인 경로 보여줌
    C -> 지정된 디렉터리에 압축풀기

    f -> 묶음 파일 이름 지정 (필수)
    v -> 묶는 과정보여줌
    J -> tar + xz
    z -> tar + gzip
    j -> tar + bzip2

    예)
    tar xvfJ 파일이름.tar.xz 
    tar xvfj 파일이름.tar.bz2
    ```

# 파일 검색

- `find`
``` bash
find /etc -name "*.conf"
find /home -user ubuntu #소유자 ubuntu 인 파일 검색
find ~ -perm 644 # 허가권이 644 인 파일검색
find /usr/bin -size +10k -size -100k # 10kb~100kb 파일검색

find ~ -size 0k -exec ls -l { } \; # 파일크기 0k 인 파일 목록 상세히 출력
find /home -name "*.swp" -exec rm { } \; # .swp 파일 찾아서 지워버리기

which
whereis
locate
```

# 예약 명령

- `cron` : 주기적인 작업 예약
```bash
분 시 일 월 요일 사용자 실행명령
00 05 1 * * root cp -r /home /backup
```

- `at` : 1회성 작업 예약
```bash
at 3:00am tomorrow
at 11:00pm January 30
at now + 1 hours

at> 프롬프트에 예약명령어 입력 후 `Enter` 입력
완료되면 ctrl + D 누르기
확인 : at -l
취소 : atrm 작업번호
```

# 네트워크 관련 명령어
- `nm-connection-editor`
- `nmtui`

위 두가지를 사용해서 수정을 한 후

- `systemctl start/stop/restart/status NetwrokManager` 로 적용

- `ipconfig` , `ip addr` : IP주소 및 정보 출력
- `nslookup` : DNS 서버 테스트
- `ping IP주소 or URL` : 네트워크 응답 테스트

# 프로세서 관련 명령어

- `파이프`
    - 2개의 프로그램을 연결해주는 연결 통로
    - `|`를 사용함
    ```bash
    ls -l /etc | less # 1페이지 씩 나눠 보겠다.
    ```

- `필터`
    - grep , tail, wc, sort, awk, sed 등이 있다.
    - 파이프와 같이 사용된다.
    ```bash
    ps -ef | grep bash  #bash 라는 글자가 들어간 프로세스만 출력
    ```

- `리디렉션`
    - 표준 입출력의 방향을 바꿔준다.
    - 표준입력은 키보드 , 출력은 모니터지만 이를 파일로 처리하고 싶을 때 사용
    ```bash
    ls -l > list.txt    # 출력을 list.txt 에 덮어쓰기
    ls -l >> list.txt   # 이어쓰기

    sort < list.txt     # list파일을 정렬해서 출력
    sort < list.txt > out.txt # list 파일을 정렬해서 out.txt 에 쓰기.
    ```

# 프로세스 , 데몬 , 서비스

- 프로세스
    - 포그라운드 프로세스 : 화면에 실행되어 보이는 프로세스
    - 백그라운드 프로세스 : 화면에 없지만 실행되고 있는 프로세스 `명령어 + &`
    - 프로세스 번호 : 프로세스 관리를 위해 부여된 고유번호
    - 작업 번호 : 백그라운드 프로세스의 순차 번호
- 부모 프로세스와 자식 프로세스
    - 예) FireFox 는 X윈도우의 자식프로세스이다.
    - 부모 프로세스가 kill 되면 자식프로세스도 자연스럽게 kill 된다.

- 명령어
    - `ps`
        - 프로세스 상태확인 `ps -e | grep 프로세스명`
    - `kill`
        - 강제 종료 `kill -9 프로세스번호`
    - `pstree` 
        - 프로세스 관계를 트리형태로 보여준다

- 서비스
    - 데몬 이라고 부르는 서비스는 서버 프로세스를 말한다.
    - `서비스` : 평상시에도 늘 가동하는 서버 프로세스
    - `소켓` : 필요할때만 작동하는 서버 프로세스
    - 위 두개는 systemd 라는 서비스 매니저 프로그램으로 작동 및 관리한다.

    - 서비스의 특징
        - 시스템과 독자적으로 구동되어 제공되는 프로세스 (웹, DB , FTP 서버등)
        - systemctl list-unit-files 로 부팅과 동시에 자동실행 관리여부 체크
        - static : 사용/사용안함 여부 설정 불가 (다른 서비스 및 소켓에 의존)

        ```bash
        systemctl start/stop/restart 서비스이름
        systemctl status 서비스이름
        systemctl enable/disable 서비스이름
        ```
    
    - 소켓의 특징
        - 항상 가동되는 서비스와 달리 외부에서 특정 서비스를 요청할 경우 systemd가 구동시킨다, 생명 주기 또한 요청이 끝나면 종료된다. (telnet 서버 등)

# 간단한 커널 컴파일

- 커널의 가장 큰 역할 : 하드웨어 지원
- 그러나, 하드웨어가 엄청 많아진 지금은 커널의 크기가 점점 커져서
- 자주 사용하지않는 기능들은 모듈로 따로 빼두게되었다.

    - 커널 업그레이드
    ```less
    -> 현 커널 버전확인(uname -r) 
    -> 커널 소스 다운로드(/usr/src) 
    -> 커널 소스 압축풀기(tar xfz linux-6.9.9.tar.gz)
    -> 커널 설정 초기화 (make mrproper)
    -> 커널 환경 설정 (make xconfig)
    -> 이전정보 삭제 (make clean)
    -> 커널 컴파일 및 설치 (make , make modules_install , make install, 
    ls -l /boot)
    -> 부트로더 확인 (cat /boot/grub/grub.cfg)
    ```

# RAID

- RAID Linear : 직렬, 순차적저장
- RAID
    - 0 : 2개이상 동시저장 (가장빠름)
    - 1 : 2개 동시저장 결함 허용제공 (Mirroring)
    - 5 : 패리티(XOR로 결함시 데이터 예측) , 3개이상
    - 6 : 2개의 패리티로 결함데이터 예측 , 4개이상

- 파티션 만들기 (VMware 로 디스크7개 생성 (SCSI))
```bash
fdisk /dev/sdb  [Disk 선택]
Command : n     [new 파티션 분할]
Select : p      [Primary]
Partition number : 1    [파티션번호]
First sector : Enter    []
Last sector : Enter     []
Command : t             [시스템 유형]
Hex Code : fd           [Linux raid autodetect 유형번호]
Command : p             [설정 내용 확인]
Command : w             [설정 내용 저장]
```
- mdadm 명령 (RAID 장치 생성 및 관리)
```bash
--create /dev/md0   # md0 장치에 RAID 생성
--level = 0         # RAID 번호
--raid-devices=2 /dev/sdb1 /dev/sdc1 #2개의 디스크를 사용
mdadm --stop /dev/md9   # md9 RAID 장치 중지
mdadm --run /dev/md9
mdadm --detail /dev/md9 # 상세내역출력
```

- 파티션 장치 파일시스템 생성 (포맷)
```bash
mkfs.ext4 /dev/md0
mkdir /raid0
mount /dev/md0 /raid0
df
```

- 부팅시 항상 마운트 되도록 설정
``` bash
nano /etc/fstab

마지막행
/dev/md0    /raid0  ext4    defaults    0   0
작성 후 저장

systemctl daemon-reload

## 최종확인
mdadm --detail /dev/md0
```

# LVM (Logical Volume Manager)
- 여러디스크 혹은 하나의 디스크를 한개의 파티션으로 구성한 후, 필요에 따라 나누는 것.

- 물리 볼륨 : 파티션을 뜻함
- 볼륨 그룹 : 물리볼륨을 모아놓은 그룹
- 논리 볼륨 : 볼륨 그룹을 1개 이상으로 나눈 것 (논리적 그룹)

- 파일 시스템 유형 : 8e

# 쿼터(Quota)

- 파일 시스템마다 사용자나 그룹이 생성할 수 있는 파일의 용량과 개수를 제한하는 것.
- Block : 1당 1KB 
- soft : soft 한도, 초과해도 복사진행됨
- hard : hard 한도, 초과할 수 없음, 초과하는 파일 존재시, 불완전한 파일이 됨
- inodes : 파일의 개수라고 이해해놓기