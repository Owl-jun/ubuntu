# ubuntu
우분투 리눅스 개인학습 저장소

## START
- VMWare 설치
    - VMware Workstation Pro 설치
    - https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion

- 설치 후
    - Use VMware Workstation 17 for Personal Use 선택
    - Create a New Virtual Machine 클릭
    - Typical
    - I will install the operating system later.
    - 그 후 설정에 맞춰서 선택
    - Edit virtual machine settings 클릭 후 하드웨어 커스터마이징 가능.

- CTRL + ALT : 마우스 사라졌을 때 단축키

- 네트워크 설정
    - Edit - Virtual Network Editor - Change Settings - Subnet IP 변경

- ISO 전송하기
    - https://www.freeisocreator.com/ 에서 다운로드 후 폴더를 지정 후 ISO 파일로 변환이 가능하다.
    - VMware 접속 후 VM - Removable Devices - CD/DVD (SATA) - Settings
    - Use ISO image file - Browse - iso 파일 선택 - Connected , Connect at power on 체크박스 체크!

- Ubuntu 다운로드
    - https://www.ubuntu.com/ 접속 후 아래 3종 다운로드
        - ubuntu 24.04.2 LTS - desktop
        - ubuntu 24.04.2 LTS - server
        - ubuntu-budgie 24.04.2 LTS - desktop
    - 폴더에 모아놓고, 설치할 VMware에 iso 등록 후 부팅
    - 쭉쭉 다음다음 누르며 설치
    - 설치 완료되면 다시시작 버튼 클릭

## SERVER         
- root 사용자 활성화
    - 바탕화면 우클릭 -> 터미널로 열기
    ```bash
    sudo su - root
    ubuntu 비밀번호 입력
    passwd
    root 비밀번호 생성 (password 2회입력)
    ```
- 우 상단 설정 탭 -> 시스템 -> 사용자 -> 자동로그인 활성화

- 터미널 및 기본세팅
    ```bash
    nano /etc/gdm3/custom.conf
    ```

    - ALT + N : 행번호 표시

    ```bash
    7행 : AutomaticLogin=ubuntu
    21행 : AllowRoot=True
    ```
    - nano 는 텍스트 편집기이다. CTRL + X 로 나가기 할 수 있다.

    ```bash
    nano /etc/pam.d/gdm-autologin
    3행 앞에 #을 붙혀 주석처리후 저장
    reboot # 재부팅
    ```

    - 좌측하단 아이콘 클릭 -> 소프트웨어 및 업데이트 -> 업데이트탭 -> 업데이트확인 및 버전알려주기 : 하지않기 로 설정.

    ```bash
    cd /etc/apt/sources.list.d/
    ls
    nano ubuntu.sources

    3행의 noble 이후 글자 지우고 저장

    apt update #모든 패키지가 최신입니다.
    ```

    - IP 주소 설정
    ```bash
    nm-connection-editor
    ```
    - netplan-ens32 선택 후 좌측하단 톱니아이콘 클릭
    - IPv4 설정 -> 추가
    ```
    주소: 192.168.111.100
    네트마스크: 255.255.255.0
    게이트웨이: 192.168.111.2
    DNS서버(네임서버): 192.168.111.2
    ```
    - 저장 후 터미널 reboot
    ```bash
    ip addr # 네트워크 정보확인
    ```

    - 화면 보호기 기능 끄기
    - 우측상단 설정 -> 전원 -> 전기절약 : 안함 설정
    - 키보드 탭 -> 입력소스 옆 `:` 아이콘 클릭 후 제거, 닫기
    - Shift + Space : 한/영 전환키

    - 필수 패키지 설치
    ```bash
    apt -y install net-tools getdit bzip2
    ```

    - 방화벽 활성화
    ```bash
    ufw enable
    ```

    - 시스템 종료
    ```bash
    halt -p
    ```

    - VMware 에서 DVD 더블클릭 후 Connect 체크해제 및 Use Physical drive 체크
    - Server 스냅숏
        - VM -> Snapshot -> Snapshot Manager
        - Take snapshot -> 생성 후 Close

## SERVER B

- live-server-amd64 iso 삽입
- 쭉쭉쭉 엔터키 눌러 진행
- 아이디 및 서버명 설정 후 쭉쭉 진행
- TEXT 모드에서 진행
    
```bash
clear
cd /etc/apt/sources.list.d/
ls
sudo nano ubuntu.sources

3행의 Suites: noble 만 남기고 뒤에 다 지우기
Ctrl + X , Y 엔터
sudo apt update 로 적용
```

```bash
ip addr # 네트워크 보기
clear
cd /etc/netplan/
ls
sudo nano 50-cloud-init.yaml
```

```bash
network:
    version: 2
    ethernets:
        ens32:
            dhcp4: no
            address: [192.168.111.200/24]
            gateway4: 192.168.111.2
            nameservers:
                addresses: [192.168.111.2]
    
```
- CTRL + X , Y , Enter
    
```bash
sudo su - root
passwd
'passwordpassword' x2회

reboot
```
