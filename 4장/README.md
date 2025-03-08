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

