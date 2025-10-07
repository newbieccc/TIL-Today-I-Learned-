# # UNIX 시스템

## 05. 리눅스 시작과 종료

- 컴퓨터과학과 김희천 교수님

### (1) 운영체제의 부팅

- 부팅 과정
    - 전원을 켜고 로그인 프롬프트가 나올 때 까지 과정
        1. ROM BIOS의 펌웨어가 실행됨
            - BIOS 기반 x86 컴퓨터를 가정
            - 하드웨어 검사 후, 부트 로더를 적재
        2. MBR에 있는 부트로더가 실행됨
            - 파티션 테이블을 조사하여 부팅 가능한 파티션을 찾음
            - 리눅스의 브트로더 GRUB를 찾아 적재함
            - GRUB는 그래픽 인터페이스와 멀티부팅을 지원
        3. 커널 이미지와 initramfs를 로드
            - 커널 이미지는 /boot/vmlinuz-<kernel-version>
            - initramfs는 부팅 과정에서 필요한 임시 파일시스템
        4. 커널이 실행됨
            - 메모리, 프로세서, 저장장치, 주변장치 등
            - 디바이스를 찾고 디바이스 드라이버를 로드함
        5. 하드웨어를 점검하고 초기화함
        6. 루트(/) 파일 시스템을 마운트하고 검사함
        7. 커널은 /lib/systemd/systemd 프로그램을 실행시키고 제어를 넘김
            - systemd 프로세스는 시스템 운영을 위한 나머지 초기화 과정을 처리
            - systemd는 부팅이 끝난 후에도 계속 수행됨
- 부팅 과정과 초기화
    1. POST
    2. BIOS
    3. 부트 로더
    4. Boot device
    5. GRUB
    6. kernel + initramfs
    7. systemd (/lib/system/systemd)
    8. /etc/systemd/system/default.target

### (2) 초기화 데몬

- 전통적 init 데몬
    - 'System V init 데몬' 이라고도 함
    - 런레벨에 따라 실행되어야 또는 중단되어야 하는 서비스가 정해짐
    - 시간이 오래 거리며, 복잡한 초기화 스크립트로 인해 새로운 하드웨어나 서비스의 등장에 효율적 대처가 어려움
- Upstart init 데몬
    - 이벤트 기반으로 서비스를 실행하는 방식
    - 복잡한 스크립트가 간단한 설정 파일들로 대체됨
    - Upstart는 Ubuntu에서 개발되어 2006년에 포함되었고 RHEL 6에서 채택됨
    - systemd 데몬은 2011년 Fedora에서 처음 채택되었음
    - RHEL 7과 SUSE 및 Ubuntu 16.04에서 systemd가 Upstart를 대체함
- systemd 프로세스
    - 커널이 실행시키는 첫 번째 사용자 프로세스
    - 모든 사용자 프로세스의 최상위 조상 프로세스(PID가 1)
        - ps -e 또는 ps ax 명령으로 확인
    - 나머지 부팅 과정, 시스템 초기화 작업을 실행함
        - '초기화 데몬'이라고 함
        - 사용자 환경을 준비함. 파일 시스템의 마운트 시스템 운영을 위한 서비스 프로그램의 실행 등
        - 서비스들의 병렬 시작, 온디맨드 활성화, 서비스 간 의존성 해결
    - 이후 계속 수행되며 시스템 운영을 관리하고 셧다운까지 처리함
        - 시스템 상태 모니터링, 데몬 관리
        - 사용자 프로세스의 정리, 로그아웃 처리와 로그인 서비스의 제공 등
- 유닛
    - systemd가 관리하는 시스템 자원이나 서비스와 같은 시스템 구성요소
    - 유닛의 동작, 의존성, 실행 옵션 등은 유닛 설정 파일에서 설정 항목으로 제어됨
    - 종류

| 유닛 유형      | 유닛 설정 파일의 확장자 | 설명                         |
|------------|---------------|----------------------------|
| `service`  | `.service`    | 시스템 서비스로 보통 데몬에 해당         |
| `target`   | `.target`     | 유닛의 그룹(예: 부팅 레벨을 표현할 때 사용) |
| `device`   | `.device`     | 커널이 인식한 디바이스 파일            |
| `mount`    | `.mount`      | 파일 시스템 마운트 지점              |
| `path`     | `.path`       | 파일 시스템의 파일 또는 디렉터리         |
| `socket`   | `.socket`     | 프로세스 간 통신에 사용되는 소켓         |
| `snapshot` | `.snapshot`   | 저장된 시스템의 상태                |

- 유닛 2
    - 유닛 파일이 존재하는 디렉터리
    - systemd 데몬의 동작에 적용되는 기본 설정은 /etc/system/system.conf 파일에 있음

| 디렉터리                       | 설명                                                    |
|----------------------------|-------------------------------------------------------|
| `/usr/lib/systemd/system/` | 소프트웨어 패키지를 설치할 때 함께 설치된 유닛 파일                         |
| `/run/systemd/system/`     | 런타임 시 만들어진 유닛 파일                                      |
| `/etc/systemd/system/`     | `systemctl enable`을 이용해 만들어진 유닛 파일. 우선 순위가 가장 높은 디렉터리 |

- 기본 타깃과 런레벨
    - 기본 타깃(부팅 모드 또는 런레벨)을 확인 또는 변경하는 명령
        - systemctl get-default 또는 systemctl set-default <name.target>
    - 초기 런레벨은 0 또는 6이 되어서는 안됨
    - 타깃과 런레벨의 비교
    - 현재 타깃을 다른 타깃 유닛으로 바꾸는 관리자 명령
        - systemctl isolate <name.target>

| 런레벨 | 타깃 유닛                                                                           | 설명                     |
|-----|---------------------------------------------------------------------------------|------------------------|
| 0   | `runlevel0.target`, `poweroff.target`                                           | 시스템을 종료하고 전원을 끔        |
| 1   | `runlevel1.target`, `rescue.target`                                             | 단일 사용자 모드로 복구 셸을 설정    |
| 2~4 | `runlevel2.target`, `runlevel3.target`, `runlevel4.target`, `multi-user.target` | 그래픽이 없는 다중 사용자 시스템을 설정 |
| 5   | `runlevel5.target`, `graphical.target`                                          | 그래픽 다중 사용자 시스템을 설정     |
| 6   | `runlevel6.target`, `reboot.target`                                             | 시스템을 종료하고 재부팅함         |

- telinit 명령
    - 런 레벨을 바꾸는 관리자 명령
    - telinit runlevel
        - telinit 3은 런레벨을 변경하여 텍스트 모드만 지원
        - telinit 0은 종료, telinit 6은 재부팅을 의미
- runlevel 명령
    - 이전 런레벨과 현재 런레벨을 확인하는 명령
- 시스템 서비스의 관리
    - 과거 서비스 수행을 초기화 스크립트는 서비스 유닛으로 대체됨
    - 관리자는 systemctl 명령을 사용하여 시스템 서비스의 상태 보기, 시작, 멈춤, 재시작, 활성화 및 비활성화 작업을 수행할 수 있음
    - `systemctl [options] <command> [units]`
        - 서브 명령으로 start, stop, reload, restart, status, enable, disable, is-active, is-enabled 등이 있음

- systemctl 명령(1)
    - 서비스 실행과 상태 확인을 위한 명령

| 명령                                          | 설명                                                       |
|---------------------------------------------|----------------------------------------------------------|
| `systemctl start name.service`              | 서비스를 시작함. `service name start`와 같음                       |
| `systemctl stop name.service`               | 서비스를 중지함. `service name stop`과 같음                        |
| `systemctl restart name.service`            | 서비스를 재시작함. `service name restart`와 같음                    |
| `systemctl try-restart name.service`        | **실행 중인 경우에만** 서비스를 재시작함. `service name condrestart`와 같음 |
| `systemctl reload name.service`             | 설정을 다시 로드함. `service name reload`와 같음                    |
| `systemctl status name.service`             | 서비스가 실행 중인지 확인함                                          |
| `systemctl is-active name.service`          | `service name status`와 유사함                               |
| `systemctl list-units --type service --all` | 모든 서비스의 상태를 출력함. `service --status-all`과 유사함             |

- systemctl 명령(2)
    - 서비스 활성화와 서비스 종속성을 확인을 위한 명령

| 명령                                                  | 설명                                                     |
|-----------------------------------------------------|--------------------------------------------------------|
| `systemctl enable name.service`                     | 서비스를 활성화하여 **부팅 시 자동 시작**되게 함. `chkconfig name on`과 같음 |
| `systemctl disable name.service`                    | 서비스를 **비활성화**함. `chkconfig name off`와 같음               |
| `systemctl status name.service`                     | 서비스의 상태 확인(활성화/비활성 포함)                                 |
| `systemctl is-enabled name.service`                 | 해당 서비스가 **enable 상태인지** 간단히 출력                         |
| `systemctl list-unit-files --type service`          | 모든 서비스를 나열하고 **활성화 여부**를 확인함. `chkconfig --list`와 유사함  |
| `systemctl list-dependencies --after name.service`  | 지정된 유닛 **이전에 시작**하도록 된 서비스들을 나열함                       |
| `systemctl list-dependencies --before name.service` | 지정된 유닛 **이후에 시작**하도록 된 서비스들을 나열함                       |

- 웹 콘솔의 사용
    - 웹 브라우저를 이용해 리눅스 서버를 관리하고 모니터링하기 위한 도구
    - cockpit 패키지 설치 후, 서비스를 활성화/시작시키고, 방화벽 설정을 확인
    - 브라우저로 `http://localhost:9090`에 접속하고 root 사용자로 로그인함

### (3) 시스템 종료

- 전원 관리 명령
    - 호환상의 이유로 shutdown 명령을 계속 사용할 수는 있음
    - 가급적 systemctl 명령을 사용하는 것이 좋음

| 명령                    | 과거 명령          | 설명                 |
|-----------------------|----------------|--------------------|
| `systemctl halt`      | `halt`         | 시스템을 종료함           |
| `systemctl poweroff`  | `poweroff`     | 시스템을 종료하고 전원을 끔    |
| `systemctl reboot`    | `reboot`       | 시스템을 재부팅함          |
| `systemctl suspend`   | `pm-suspend`   | 시스템을 일시 중단함        |
| `systemctl hibernate` | `pm-hibernate` | 시스템을 최대 절전 모드로 전환함 |

- shutdown 명령
    - 시간을 정해 시ㅣ스템을 안전하게 종료하는 명령
    - `shutdown [options] time [message]`
    - 옵션
        - -r은 재부팅, -c는 예약된 셧다운의 취소(time 인수가 필요 없음)
        - -k는 실제 셧다운을 하는 것처럼 경고 메시지만 보냄
        - shutdown -r +10
        - time 인수
            - 종료 시간으로 23:15은 절대 시간 형식, +10은 10분 후 종료를 의미
            - shutdown -H 23:15 또는 shutdown -P +10
            - 인수로 now는 즉시 종료를 의미
            - shutdown -h now
- 시스템의 종료 절차
    - 실제 systemd 프로세스를 통해 셧다운이 처리됨
        - systemd 프로세스는 모든 프로세스에게 종료를 알림
        - 각 프로세스가 스스로 종료하도록 TERM 시그널을 보냄
        - 종료하지 않은 프로세스에게 강제 종료를 위한 KILL 시그널을 보냄
        - 파일 시스템을 잠그고 루트 파일 시스템을 제외한 모든 파일 시스템을 언마운트함
        - 시스템 호출을 통해 커널에 재부팅 또는 종료를 요청함
    - 종료를 위해 halt 명령을, 재부팅을 위해 reboot 명령을 사용할 수도 있음

- 시스템의 일시 중단
    - systemctl suspend
        - 일시 중담: 시스템 상태를 RAM에 저장하고 저전력 상태로 함
    - systemctl hibernate
        - 최대 절전모드: 시스템 상태를 하드디스크에 저장하고 전원을 끔
    - systemctl hybrid-sleep
        - 하이브리드 슬립: 메모리 외에 디스크에도 시스템 상태를 저장함

### (4) 데스크톱

- 데스크톱
    - GUI를 제공하는 사용자 환경
        - 그래픽 윈도우, 아이콘 툴바, 메뉴, 위젯 등을 마우스나 키보드로 조작
    - 대부분의 데스크톱은 X 윈도우 시스템에 기반을 둠
    - 시각적으로 다양한 스타일의 데스크톱이 존재함
        - 일반적으로 서버로 사용하는 리눅스에서는 명령 행 인터페이스만 제공
- GNOME
    - Red Hat 계열 리눅스에서 기본 데스크톱임
    - 단숨함, 편의성, 안정성에 초점을 맞춤
        - 상단 좌측에 [현재 활동] 버튼 클릭하면 '활동 개요' 화면
        - 여러 작업 공간을 선택할 수 있음
    - 미니멀한 사용자 인터페이스가 특징
- KDE
    - 'K 데스크톱'이라고도 하며 MS 윈도우 환경과 유사
    - 다양한 프로그램을 통합적인 모습으로 보여줌
    - yum -y groupinstall 'KDE Plasma Workspaces'으로 설치할 수 있음
    - 로그인할 때 'GNOME'또는 'KDE'를 선택할 수 있음
