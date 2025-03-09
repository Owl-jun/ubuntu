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