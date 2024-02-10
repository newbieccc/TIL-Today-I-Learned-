# 정보처리기사 2024

## # 4-3. 프로그래밍 언어 활용 - 응용 SW 기초 기술 활용

### # 1. 운영체제 기초 활용 4-117page

### 4. UNIX에서 새로운 프로세스를 생성하는 명령어

- `fork`
- ls : 자신이 속해있는 폴더 내에서의 파일 및 폴더들의 목록(list)을 표시하는 명령어
- cat : 파일의 내용을 화면에 출력하는 명령어
- fork : 새로운 프로세스를 생성하는 명령어
- chmod : 특정 파일 또는 디렉토리의 퍼미션을 수정하는 명령어

### 6. 지역성(Locality)에 대한 설명

- 프로세서들은 기억장치 내의 정보를 균일하ㅔㄱ 접근하는 것이 아니라, 어느 한 순간에 특정 부분을 집중적으로 참조한다.
- 시간 지역성의 예는 "순환, 부 프로그램, 스택"등 이 있다.
- 공간 지역성은 하나의 기억장소가 참조되면 그 근처의 기억 장소가 참조되는 경향이 있음을 의미하는 지역성이다.

### 7. FIFO 페이지 교체 알고리즘을 사용할 경우 페이지 결함의 발생 횟수

```markdown
- 4개의 프레임을 수용할 수 있는 주기억장치가 있으며,
- 초기에는 모두 비어 있다고 가정한다.
- 다음의 순서로 페이지 참조가 발생할 때,
- FIFO 페이지 교체 알고리즘을 사용할 경우 페이지 결함의 발생 횟수는?
- 페이지 참조 순서 : 1, 2, 3, 1, 2, 4, 5, 1, 4
```

- `6회`
- 주기억장치 페이지에 순차적으로 참조 스트링이 들어오고 페이지 교체는 가장 먼저 들어온 페이지부터 교체

|참조 스트링|1|2|3|1|2|4|5|1|4|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|주기억 장치</br>(페이지 프레임)|1|2|3|3|3|4|5|1|1|
|||1|2|2|2|3|4|5|5|
||||1|1|1|2|3|4|4|
|||||||1*|2*|3|3|
|페이지 부재</br>(Page Fault)|f|f|f||||f|f|f|

- 주기억 장치에 참조 스트링이 없으면 페이지 부재(f)가 일어나고, 새로운 값이 들어온다.
- 5가 없으므로 페이지 부재가 일어나고, 가장 먼저 들어온 1이 빠지고, 5가 들어온다.
- 페이지 부재(f) : 6회
- '*' : 교체 대상

### 10. 작업 시간의 평균 반환시간

```markdown
FIFO 스케줄링에서 3개의 작업 도착시간과 CPU 사용 시간(Burst Time)이 다음 표와 같다. 이때 모든 작업들의 평균 반환시간(Turn Around time)은 얼마인가? (소수점 이하는 반올림 처리.)
```

|작업|도착시간|CPU 사용시간</br>(Burst Time)|
|:--:|:--:|:--:|
|JOB 1|0|13|
|JOB 2|3|35|
|JOB 3|8|2|

- `33`
- 평균 반환시간 = (13+45+42)/3=33 (소수점 이하 반올림 처리)

|작업|도착시간|CPU 사용시간</br>(Burst Time)|종료 시간|반환 시간|
|:--:|:--:|:--:|:--:|:--:|
|JOB 1|0|13|13|13(13-0)|
|JOB 2|3|35|48|45(48-3)|
|JOB 3|8|2|50|42(50-8)|

### 11. 메모리 관리 기법 중 할당

- '메모리 관리 기법 중 Worst Fit 방법을 사용할 경우 10K크기의 프로그램 실행을 위해서는 어느 부분에 할당 되는가?'

|영역번호|메모리 크기|사용 여부|
|:--:|:--:|:--:|
|No.1|8K|FREE|
|No.2|12K|FREE|
|No.3|10K|IN USE|
|No.4|20K|IN USE|
|No.5|16K|FREE|

- `No.5`

- 최악 적합(Worst Fit) 방법은 프로세스의 가용 공간 중에서 가장 큰 공간을 할당하는 방식이다.
- 문제에서 10K 크기의 프로그램이라고 하였으므로 No.2, No.3, No.4, No.5 영역 중 메모리 크기가 20K로 가장 큰 No.4가 할당되어야 하나 사용 여부가 IN USE 이므로 그 다음으로 메모리 크기가 큰 NO.5에 할당한다.

### 14. 페이징 기번에서 페이지 크기가 작아질수록 발생하는 현상

- 기억장소 이용 효율이 증가한다.
- 입,출력 시간이 늘어난다.
- 내부 단편화가 감소한다.
</br>
- 페이지 크기가 작을 경우 발생 현상
  - 더 많은 페이지 사상 테이블 공간이 필요
  - 내부 단편화는 줄고, 특정한 참조 구역성만을 포함하기 때문에 기억 장치 효율이 좋음
  - 페이지 정보를 갖는 페이지 맵 테이블의 크기가 커지고, 매핑 속도가 늦어짐
  - 디스크 접근 횟수가 많아져서 전체적인 입,출력 시간 증가
- 페이지 크기가 클 경우 발생 현상
  - 테이블의 크기가 작아지므로 주기억 장치의 공간이 절약
  - 페이지 정보를 갖는 페이지 맵 테이블의 크기가 작아져서 관리가 용이하고, 매핑 속도가 빨라짐
  - 디스크 접근 횟수가 줄고, 전체적인 입,출력 시간 감소
  - 페이지 단편화가 증가하고, 이에 따라 기억 공간의 낭비 초래

### 15. 페이지 교체 (Page Replacement) 알고리즘

- FIFO(First-In-First-Out)
  - 각 페이지가 주기억 장치에 적재될 때마다 그때의 시간을 기억시켜 가장 먼저 들어와 가장 오래 있던 페이지를 교체하는 기법(선입선출)
- OPT(OPTimal Replacement)
  - 앞으로 가장 오랫동안 사용하지 않을 페이지를 교체하는 기법
  - 페이지 부재 횟수가 가장 적게 발생하는 가장 효율적인 알고리즘
- LRU(Least Recently Used)
  - 사용된 시간을 확인하여 가장 오랫동안 사용되지 않은 페이지를 선택하여 교체하는 기법
  - 프로그램의 지역성의 원리에 따라서 최근에 참조된 페이지는 앞으로도 참조될 가능성이 크고, 최근에 참조되지 않은 페이지는 앞으로도 참조되지 않을 가능성이 크다는 전제로 구현된 알고리즘

### 19. 프로세스가 실행되면서 하나의 페이지를 일정시간동안 집중적으로 액세스하는 현상

- `구역성(Locality)`

|||
|:--:|--|
|Locality</br>(구역성, 지역성)|실행 중인 프로세스가 주기억장치를 참조할 때 일부 페이지만 집중적으로 참조하는 성질|
|Thrasing</br>(스레싱)|프로세스의 처리 시간보다 페이지 교체 시간이 더 많아지는 현상|
|Working Set</br>(워킹 셋)|프로세스가 일정 시간동안 자주 참조하는 페이지들의 집합|
|Prepagin</br>(프리페이징)|사용될 페이지라고 예측되어지는 페이지를 미리 적재하는 기법|

### 20. HRN 방식으로 스케즐링할 경우, 입력된 작업이 다음과 같을 때 처리되는 작업 순서로 옳은 것은

|작업|대기시간|서비스(실행) 시간|
|:--:|:--:|:--:|
|A|5|20|
|B|40|20|
|C|15|45|
|D|20|2|

- `D->B->C->A`
- HRN(Higest Response Ratio Next)의 공식은'(대기시간 + 서비스 시간)/서비스 시간'이다.
- A : (5+20)/20=1.25
- B : (40+20)/20=3
- C : (15+45)/45=1.34
- D : (20+2)/2=11

### 21. HRN 스케줄링 방식에 대한 설명

- HRN(Highesst Response-ratio Next)
  - 대기시간이 긴 프로세스일 경우 우선순위가 높아진다.
  - SJF 기법을 보완하기 위한 방식이다.
  - 긴 작업과 짧은 작업 간의 지나친 불평등을 해소 할 수 있다.
  - 우선순위를 계산하여 그 수치가 가장 높은 것부터 순서대로 우선순위가 부여된다.

### 23. 다음의 설명으로 해당하는 것은?

- 운영체제의 운용 기법 중 중앙처리 장치의 시간을 각 사용자에게 균등하게 분할하여 사용하는 체제로서 모든 컴퓨터 사용자에게 똑같은 서비스를 제공하는 것을 목표로 삼고 있으며, 라운드 로빈 스케줄링을 사용하는 것은?
  - Time Sharing System

|||
|:--:|:--:|
|Real-Time Processing System|실시간 처리 시스템|
|Time Sharing System|시분할 시스템|
|Batch Processing System|일괄처리 시스템|
|Distributed Processing System|분산처리 시스템|

### 27. 비선점(Non-Preemptive) 스케줄링에 해당하는 것은?

- 비선점 스케줄링 알고리즘 (우기 HFS)
  - 우선순위
  - 기한부
  - HRN
  - FCFS
  - SJF
- 선점 스케줄링 알고리즘 (SMMF)
  - SRT
  - MLQ
  - MLFQ
  - Round Robin

### 28. SJF(Shortest-Job-First) 스케줄링 방법에 대한 설명

- SJF(Shortest-Job-First) 스케줄링 방법
  - 프로세스가 도착하는 시점에 따라 그 당시 가장 작은 서비스 시간을 갖는 프로세스가 종료 시까지 자원을 점유하는 방식이다.
  - 준비 큐 작업 중 가장 짧은 작업부터 수행, 평균 대기시간이 최소가 된다.
  - 기아 현상(Starvation) 발생 가능성이 있따.
  - 남은 처리 시간이 더 짧다고 판단되는 프로세스가 준비 큐에 생기면 언제라도 프로세스가 선점되는 방식이다.

```markdown
최단 작업 우선 스케줄링 (Shortest Job First Scheduling)
- 평균 대기시간을 최소화하기 위해 CPU 점유 시간이 가장 짧은 프로세스에 CPU를 먼저 할당하는 방식의 CPU 스케줄링을 알고리즘으로 평균 대기시간을 최소로 만드는 알고리즘이다.
```

### 30. 프로세스 적재 정책과 관련한 설명

- 프로세스 적재 정책과 관련한 설명
  - 반복, 스택, 부프로그램은 시간 지역성(Temporal Locality)과 관련이 있다.
  - 공간 지역성(Spatial Locality)은 프로세스가 어떤 페이지를 참조했다면 이후 가상주소 공간상 그 페이지와 인접한 페이지들을 교환할 가능성이 높음을 의미한다.
  - 스레싱(Thrashing) 현상을 방지하기 위해서는 각 프로세스가 필요로 하는 프레임을 제공할 수 있어야 한다.

- 스레싱(Thrashing)은 어떤 프로세스가 계속적으로 페이지 부재가 발생하여 프로세스의 실제 처리 시간보다 페이지 교체 시간이 더 많아지는 현상이다.
- 스레싱(Thrashing) 현상을 방지하기 위해서는 각 프로세스가 많이 참조하는 페이지들의 집합을 주기억 장치 공간에 계속 상주하게 하여 빈번한 페이지 교체 현상을 줄이고자 하는 기법인 워킹 세트(Working Set)와 페이지 부재 비율에 따라 페이지 프레임 개수를 조절하는 페이지 부재 빈도(PFF; Page-Fault Frequency)기법이 있다.

||||
|:--:|--|--|
|시간</br>(Temporal)</br>지역성|- 최근 사용되었던 기억 장소들이 집중적으로 엑세스하는 현상</br>- 참조했던 메모리는 빠른 시간에 다시 참조될 확률이 높은 특성|- Loop(반복, 순환), 스택(Stack), 부프로그램(Sub Routine), Counting(1씩 증감), 집계(Totaling)에 사용 되는 변수(기억 장소)|
|공간(Spatial)</br>지역성|- 프로세스 실행 시 일정 위치의 페이지를 집중적으로 액세스하는 현상</br>- 참조된 메모리 근처의 메모리를 참조하는 특성|- 배열 순회, 프로그래머들이 관련된 변수(데이터 저장 기억 장소)들을 서로 근처에 선언하여 할당되는 기억 장소, 가은 영역에 있는 변수 참조|
|순차</br>(Sequential)</br>지역성|- 데이터가 순차적으로 액세스되는 현상</br>- 프로그램 내의 명령어가 순차적으로 구성된 특성</br>- 공간 지역성에 편입되어 설명되기도 함|- 순차적 코드 실행|

### 31. 다음의 설명에 해당하는 의미

- 운영체제의 가상기억장치 관리에서 프로세스가 일정 시간동안 자주 참조하는 페이지들의 집합을 의미하는 것은?
  - Working Set
- 워킹 세트(Working Set)
  - 각 프로세스가 많이 참조하는 페이지들의 집합을 주기억장치 공간에 계속 상주하게 하여 빈번한 페이지 교체 현상을 줄이고자 하는 기법
- 지역성(Locality; 구역성)
  - 프로세스가 기억 장치 내의 모든 정보를 균일하게 참조하는 것이 아니라 특정 부분만을 집중적으로 참조하는 성질
- 교착상태(Deadlock)
  - 다중프로세싱 환경에서 두 개 이상의 프로세스가 특정 자원할당을 무한정 대기하는 상태
- 스레싱(Thrashing)
  - 프로세스의 처리 시간보다 페이지 교체시간이 더 많아지는 현상

### 32. 프로세스 상태의 종류

- 프로세스 상태 (생준 실대완)
  - 생성(Create) 상태
  - 준비(Ready) 상태
  - 실행(Running) 상태
  - 대기(Waiting) 상태
  - 완료(Complete) 상태
- Request는 프로세스 상태의 종류에 해당하지 않는다.
- Exit는 완료(종료) 상태를 의미한다.

### 35. 운영체제에서 스레드(Thread)의 개념

- 운영체제에서 스레드(Thread)의 개념
  - 다중 프로그래밍 시스템에서 CPU를 받아서 수행되는 프로그램 단위이다.
  - 프로세스(Process)나 태스크(Task)보다 더 작은 단위이다.
  - 한 태스크(Task)는 여러 개의 스레드(Thread)로 나누어 수행될 수 있다.
- 스레드는 입출력 장치가 아닌 CPU 자원 할당에 관계된다.
- 스레드는 프로세스에서 실행 제어만 분리한 실행 단위로 한개의 프로세스는 여러 개의 스레드를 가질 수 있따.

### 38. 교착상태의 해결방법 중 회피(Avoidance) 기법과 밀접한 관계는?

- 회피기법
  - 흔행가 알고리즙
  - Wound-Wait
  - Wait-Die

### 40. 교착상태가 발생할 수 있는 조건

- 교착상태가 발생할 수 있는 조건
  - 상호배제 (Mutual Exclusive)
    - 프로세스가 자원을 배타적으로 점유하여 다른 프로세스가 그 자원을 사용할 수 없음
  - 점유와 대기 (Hold & Wait)
    - 한 프로세스가 자원을 점유하고 있으면서 또 다른 자원을 요청하고 대기하고 있는 상태
  - 비선점 (Non Preemption)
    - 한 프로세스가 점유한 자원에 대해 다른 프로세스가 선점할 수 없고, 오직 점유한 프로세스만이 해제 가능
  - 환형 대기 (Circular Wait)
    - 두 개 이상의 프로세스 간 자원의 점유와 대기가 하나의 원형을 구성한 상태

### 43. 리눅스 Bash 쉡(Shell)에서 export와 관련한 설명

- 리눅스 Bash 쉡(Shell)에서 export와 관련한 설명
  - export가 매개변수 없이 쓰일 경우 현재 설정된 환경 변수들이 출력된다.
  - 사용자가 생성하는 변수는 export 명령어로 표시하지 않는 한 현재 쉡에 국한된다.
  - 변수를 export 시키면 전역(Global) 변수처럼 되어 끝까지 기억된다.

```markdown
- env, set, printenv 명령어들은 변수 없이 사용하면, 모든 환경 변수 및 그에 따른 모든 값을 보여 준다.
- env와 set은 환경 변수를 설정하는 데 쓰일 수도 있으며 쉘에 직접 통합되기도 한다.
- printenv는 변수 이름을 명령어에 단일 변수로 주면, 하나의 단일 변수 인쇄에 쓰일 수 있다.
```

### 44. UNIX SHELL 환경 변수를 출력하는 명령어

- UNIX SHELL 환경 변수를 출력하는 명령어
  - printenv
  - env
  - setenv

```markdown
- env, set, 그리고 printenv 명령어들은 UNIX SHELL 환경 변수를 출력하는 명령어이다.
- setenv는 csh와 관련된 쉘에서 쓰인다.
```

### 45. 운영체제 커널의 기능

- 운영체제 커널의 기능
  - 프로세스 생성, 종료
  - 기억장치 할당, 회수
  - 파일 시스템 관리

```markdown
- 쉘은 운영체계의 가장 바깥 부분에 위치해서 사용자 명령에 대한 처리를 담당하는 역할을 하고, 인터페이스 기능을 수행한다.
```

- 커널의 기능
  - 프로세스 관리
    - 프로세스 스케줄링 및 동기화 관리 담당
    - 프로세스 생성과 제거, 시작과 정지, 메시지 전달 등의 기능 담당
  - 기억장치 관리
    - 프로세스에게 메모리 할당 및 회수 관리 담당
  - 주변장치 관리
    - 입출력 장치 스케줄링 및 전반적인 관리 담당
  - 파일 관리
    - 파일 관리 파일의 생성과 삭제, 변경, 유지 등의 관리 담당

### 46. SSTF 스케줄링을 사용한 경우의 처리 순서

- 사용자가 요청한 디스크 입,출력 내용이 다음과 같은 순서로 큐에 들어 있을 때 SSTF 스케줄링을 사용한 경우의 처리 순서는? (단, 현재 헤드 위치는 53이고, 제일 안쪽이 1번, 바깥쪽이 200번 트랙이다.)
  - 큐의 내용 : 98 183 37 122 14 124 65 67
  - 이동 순서 -> 53 65 67 37 14 98 122 124 183

```markdown
- SSTF는 현재 위치에서 탐색 거리(Seek Distance)가 가장 짧은 트랙에 대한 요청을 먼저 서비스하는 기법으로 현재 헤드 위치에서 가장 가까운 거리에 있는 트랙으로 헤드를 이동시킨다. 
```

### 48. UNIX 시스템의 쉘(Shell)의 주요 기능에 대한 설명

- UNIX 시스템의 쉘(Shell)의 주요 기능에 대한 설명
  - 사용자 명령을 해석하고 커널로 전달하는 기능을 제공한다.
  - 반복적인 명령을 프로그램으로 만드는 프로그래밍 기능을 제공한다.
  - 초기화 파일을 이용해 사용자 환경을 설정하는 기능을 제공한다.
- 쉘 프로그램 실행을 위해 프로세스와 메모리 관리하는 기능을 제공하는 것은 커널이다.

### 50. 다음 설명에 해당하는 것

- 사용자 수준에서 지원되는 스레드(Thread)가 커널에서 지원되는 스레드에 비해 가지는 장점으로 옳은 것
  - 커널 모드로의 전환 없이 스레드 교환이 가능하므로 오버헤드가 줄어든다.

```markdown
- 여러개의 사용자 스레드 중 하나의 스레드가 시스템 호출등으로 블록이 걸리면 나머지 모든 스레드 역시 블록 된다.
- 커널 레벨 스레드는 커널이 각 스레드를 개별적으로 관리할 수 있다.
- 사용자 레벨 스레드는 커널 모드로의 전환 없이 스레드 교환이 가능하므로 오버헤드가 줄어든다.
```

---

### # 2. 네트워크 기초 활용 4-162page

### 1. MAC 기능 지원을 채택한 것은?

- IEEE 802.11 워킹 그룹의 무선 LAN 표준화 현황 중 QoS 강화를 위해 MAC 기능 지원을 채택한 것은?
  - 802.11e
- 802.11a
  - 5GHz 대역에서 54Mbps 속도를 제공
- 802.11b
  - 2.4GHz 대역에서 11Mbps 속도를 제공
- 802.11g
  - 802.11b와 속도가 향상(22Mbps 이상)
- 802.11e
  - QoS강화를 위해 MAC 지원 기능을 채택
  - 초고속 서비스(IP 전화, 비디오)에 QoS를 제공

### 3. 다음 설명에 해당하는 방식은?

```markdown
- 무선 랜에서 데이터 전송 시, 매체가 비어있음을 확인한 뒤 충돌을 회피하기 위해서 임의 시간을 기다린 후 데이터를 전송하는 방법이다.
- 네트워크에 데이터의 전송이 없는 경우라도 동시 전송에 의한 충돌에 대비하여 확인 신호를 전송한다.
```

- `CSMA/CA`
- 통신망 사용시 공유 매체에 대한 다중 접근제어 방식
  - CSMA/CD(Carrier Sense Multiple Access with Collision Detection; 반송파 감지 다중 접속 / 충돌탐지)
    - IEEE802.3 유선 LAN의 반이중 방식(Half Duplex)에서 사용하는 방식으로 각 단말이 신호 전송 전에 현재 채널이 사용 중인지 체크하여 사용하지 않을 때 전송하는 전송매체 접속 제어(MAC) 방식
  - CSMA/CA(Carrier Sense Multiple Access with Collision Avoidance; 반송파 감지 다중 접속 / 충돌 회피)
    - IEEE 802.11 무선 LAN의 반이중 방식(Half Duplex)에서 사용하는 방식으로 데이터 전송 시, 매체가 비어 있음을 확인한 뒤 충돌을 회피하기 위해서 임의 시간을 기다린 후 데이터를 전송하는 방법

### 4. 다음에 해당하는 계층은?

- OSI 7계층에서 단말기 사이에 오류 수정과 흐름 제어를 수행하여 신뢰성 있고 명확한 데이터를 전달하는 계층은?
  - `전송 계층`
- 전송 계층
  - 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 ㅇ낳도록 해주면서 양 끝단(End to End)의 사용자들에게 신뢰성 있는 데이터를 전달하는 계층이다.
    - 순차 번호 기반의 오류 제어 방식을 사용한다.
    - 종단 간 통신을 다루는 최하위 계층으로 종단 간 신뢰성 있고 효율적인 데이터를 전송한다.
    - 단위는 세그먼트이다.
    - 주요 프로토콜은 TCP, UDP이다.

### 5. OSI 7계층에서 TCP는 어떤 계층에 해당하는가?

- OSI 7계층에서 TCP는 어떤 계층에 해당하는가?
  - 전송계층
- TCP는 전송계층의 프로토콜이고, IP는 네트워크 계층의 프로토콜이다.

### 6. 다음에 해당하는 계층은?

- OSI 7계층에서 종단 간 신뢰성 있고 효율적인 데이터를 전송하기 위해 오류 검출과 복구, 흐름 제어를 수행하는 계층은?
  - 전송 계층
- 전송계층
  - 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해주면서 종단 간의 사용자들에게 신뢰성 있는 데이터를 전달하는 계층
- 세션 계층
  - 응용 프로그램 간의 대화를 유지하기 위한 구조를 제공하고, 이를 처리하기 위해 프로세스들의 논리적인 연결을 담당하는 계층
- 표현계층
  - 애플리케이션이 다루는 정보를 통신에 알맞은 형태로 만들거나 하위 계층에서 온 데이터를 사용자가 이해할 수 있는 형태로 만드는 역할을 담당하는 계층
- 응용 계층
  - 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행하는 계층

### 7. 다음에 해당하는 계층은?

- OSI 7 Layer에서 링크의 설정과 유지 및 종료를 담당하며, 노드 간의 오류 제어와 흐름 제어 기능을 수행하는 계층은?
  - `데이터 링크 계층`
- 응용 계층
  - 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행하는 계층
- 표현 계층
  - 애플리케이션이 다루는 정보를 통신에 알맞은 형태로 만들거나 하위 계층에서 온 데이터를 사용자가 이해할 수 있는 형태로 만드는 역할을 담당하는 계층
- 세션 계층
  - 응용 프로그램 간의 대화를 유지하기 위한 구조를 제공하고, 이를 처리하기 위해 프로세스들의 논리적인 연결을 담당하는 계층
- 전송 계층
  - 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해주면서 종단 간의 사용자들에게 신뢰성 있는 데이터를 전달하는 계층
- 네트워크 계층
  - 다양한 길이의 패킷을 네트워크를 통해 전달하고 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 위한 수단을 제공하는 계층
- 데이터 링크 계층
  - 링크의 설정과 유지 및 종료를 담당하며, 노드 간의 오류 제어와 흐름 제어 기능을 수행하는 계층
- 물리 계층
  - 실제 장치들을 연결하기 위해 필요한 전기적, 물리적 세부 사항들을 정의하는 계층

### 8. 다음에 해당하는 계층은?

- OSI 7계층에서 물리적 연결을 이용해 신뢰성 있는 정보를 전송하려고 동기화, 오류 제어, 흐름 제어 등의 전송에러를 제어하는 계층은?
  - `데이터 링크 계층`
    - 링크의 설정과 유지 및 종료를 담당하며 물리적 연결을 이용해 신뢰성 있는 정보를 전송하려고 동기화, 오류 제어, 흐름 제어, 회선 제어 기능을 수행하는 계층이다.

### 9. OSI 7계층 중 네트워크 계층에 대한 설명

- OSI 7계층 중 네트워크 계층에 대한 설명
  - 패킷을 발신지로부터 최종 목적지까지 전달하는 책임을 진다.
  - 패킷에 발신지와 목적지의 논리 주소를 추가한다.
  - 라우터 또는 교환기는 패킷 전달을 위해 경로를 지정하거나 교환 기능을 제공한다.
- 프레임은 OSI 7계층 중 데이터링크 계층의 데이터의 단위이다.

```markdown
OSI 7계층 중 네트워크 계층의 특징
- 패킷을 발신지로부터 최종 목적지까지 전달하는 책임을 짐
- 패킷에 발신지와 목적지의 논리 주소를 추가함
- 라우터 또는 교환기는 패킷 전달을 위해 경로를 지정하거나 교환 기능을 제공
- 네트워크 계층은 다양한 길이의 패킷을 네트워크들을 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 위한 수단을 제공하는 계층임
- 네트워크 계층은 라우팅, 패킷 포워딩, 인터 네트워킹(Inter-Networking)등을 수행
```

### 10. 오류 제어에 사용되는 자동반복 요청 방식(ARQ)

- 오류 제어에 사용되는 자동반복 요청 방식(ARQ)
  - Stop-and-wait ARQ 방식
    - 한 개의 프레임을 전송하고, 수신 측으로부터 ACK 및 NAK 신호를 수신할 때까지 정보 전송을 중지하고 기다리는 방식
    - 송신 측이 수신 측으로부터 ACK를 받으면 다음 프레임을 전송하고, NAK를 받으면 재전송
    - 데이터 프레임의 정확한 수신 여부를 매번 확인 하면서 다음 프레임을 전송해나가는 가장 간단한 오류 제어 방식
    - 구현이 간단하고 송신측에서 최대 프레임 크기의 버퍼가 1개만 있어도 됨
    - 전송시간이 긴 경우 전송효율이 저하
  - Go-back-N ARQ 방식
    - 데이터 프레임을 연속적으로 전송하는 과정에서 NAK를 수신하게되면, 오류가 발생한 프레임 이후에 전송된 모든 데이터 프레임을 재전송하는 방식
  - Selective repeat ARQ 방식
    - 연속적으로 데이터 프레임을 전송하고 에러가 발생한 데이터 프레임만 재전송하는 방식

### 11. CIDR(Clasless Inter-Domain Routing) 표기로 203.241.132.82/27과 같이 사용 되었다면, 해당 주소의 서브넷 마스크(subnet mask)는?

- /27이므로 서브넷 마스크는 1을 27개 채운 주소이다.
  - 2진수 : 11111111.11111111.11111111.11100000
  - 10진수 : 255.255.255.224

### 12. 200.1.1.0/24 네트워크를 FLSM 방식을 이용하여 10개의 subnet으로 나누고 ip subnet-zero를 적용했다. 이때 서브네팅된 네트워크 중 10번째 네트워크의 broadcast IP 주소는?

- `200.1.1.159`
- IP 주소를 2진수로 바꾸면 다음과 같다.
  - 10진수 : 200.1.1.0
  - 2진수 : 11001000.00000001.00000001.00000000
- /24이므로 서브넷 마스크는 1을 24개 채운다
  - 2진수 : 11111111.11111111.11111111.00000000
- IP 주소와 서브넷 마스크를 AND 연산한 결과가 네트워크 주소이다.

```markdown
    11001000.00000001.00000001.00000000
  & 11111111.11111111.11111111.00000000
    -----------------------------------
    11001000.00000001.00000001.00000000 
```

- 10개의 subnet으로 나누기 때문에 2n>=10을 만족하는 n은 4이므로 서브넷 마스크 중 25번째 비트~ 28번째 비트(4비트)는 subnet을 위해 사용한다.

```markdown
1번째 서브넷 : 11001000.00000001.00000001.00000000
2번째 서브넷 : 11001000.00000001.00000001.00010000
3번째 서브넷 : 11001000.00000001.00000001.00100000
4번째 서브넷 : 11001000.00000001.00000001.00110000
5번째 서브넷 : 11001000.00000001.00000001.01000000
6번째 서브넷 : 11001000.00000001.00000001.01010000
7번째 서브넷 : 11001000.00000001.00000001.01100000
8번째 서브넷 : 11001000.00000001.00000001.01110000
9번째 서브넷 : 11001000.00000001.00000001.10000000
10번째 서브넷 : 11001000.00000001.00000001.10010000
```

- 10번째 서브넷은 11001000.00000001.00000001.10010000이고, 호스트 ID는 29번째 비트~32번째 비트(4비트)이다. (브로드캐스트일때 호스트 ID는 모두 1로 채움)
- 10번째 서브넷 브로드캐스트 IP주소 : 11001000.00000001.00000001.10011111
- 10번쨰 서브넷 브로드캐스트 IP 주소의 10진수는 -> 200.1.1.159이다.

### 13. 192.168.1.0/24 네트워크를 FLSM 방식을 이용하여 4개의 Subnet으로 나누고 IP Subnet-zero를 적용했다. 이때 Subnetting 된 네트워크 중 4번째 사용 가능한 IP는 무엇인가?

- `192.168.1.196`
- IP주소를 2진수로 바꾸면 다음과 같다.
  - 10진수 : 192.168.1.0
  - 2진수 : 11000000.10101000.00000001.00000000
- /24이므로 서브넷 마스크는 1을 24개 채운다
  - 2진수 : 11111111.11111111.11111111.00000000
- IP 주소와 서브넷 마스크를 AND 연산한 결과가 네트워크 주소이다.

```markdown
    11000000.10101000.00000001.00000000
  & 11111111.11111111.11111111.00000000
    -----------------------------------
    11000000.10101000.00000001.00000000 
```

- 4개의 subnet으로 나누기 때문에 2n>=4를 만족하는 n은 2이므로 서브넷 마스크 중 25번째 비트~26번째 비트(2비트)는 subnet을 위해 사용한다.

```markdown
1번째 서브넷 : 11000000.10101000.00000001.00000000
2번째 서브넷 : 11000000.10101000.00000001.01000000
3번째 서브넷 : 11000000.10101000.00000001.10000000
4번째 서브넷 : 11000000.10101000.00000001.11000000
```

- 11000000.10101000.00000001.11000000은 네트워크 주소이고 11000000.10101000.00000001.11111111은 브로드캐스트 주소이므로 제외한다.

```markdown
4번째 서브넷 1번째 IP 주소 : 11000000.10101000.00000001.11000001
4번째 서브넷 2번째 IP 주소 : 11000000.10101000.00000001.11000010
4번째 서브넷 3번째 IP 주소 : 11000000.10101000.00000001.11000011
4번째 서브넷 4번째 IP 주소 : 11000000.10101000.00000001.11000100
```

- 4번째 서브넷 4번째 IP 주소는 11000000.10101000.00000001.11000100이므로 10진수로 192.168.1.196이다.

### 15. IPv6에 대한 설명

- IPv6에 대한 설명
  - 128비트의 주소 공간을 제공한다.
  - 인증 및 보안 기능을 포함하고 있다.
  - IPv6 확장 헤더를 통해 네트워크 기능확장이 용이하다.
  - IPv6의 헤더 크기가 고정되어 있다.
  - 패킷 크기는 최대 65,535바이트(64KBye-1Byte)까지 가능하다.

### 16. IPv6의 주소체계 전송방식

- IPv6의 주소체계 전송방식 (유멀애)
  - 유니캐스트
  - 멀티캐스트
  - 애니캐스트

### 18. C class에 속하는 IP address

- `200.168.30.1`
- A클래스 : 0.0.0.0 ~ 127.255.255.255
- B클래스 : 128.0.0.0 ~ 191.255.255.255
- C클래스 : 192.0.0.0 ~ 223.255.255.255
- D클래스 : 224.0.0.0 ~ 239.255.255.255
- E클래스 : 240.0.0.0 ~ 255.255.255.255

### 25. 라우팅 프로토콜

- 라우팅 프로토콜
  - BGP (Border Gateway Protocol)
  - OSPF (Open Shortest Path First)
  - RIP (Routing Information  Protocol)
- SLIP (Serial Line Internet Protocol)
  - 전화 회선, RS-232 등의 직렬 인터페이스를 이용하여 인터넷에 접속하는 다이얼 업 IP 접속을 위한 업계 표준 규약이다.

### 26. UDP 특성

- UDP 특성
  - 흐름 제어나 순서 제어가 없어 전송 속도가 빠르다.
  - 데이터 전송 전 연결 성정하지 않는 비연결형 서비스 제공
  - TCP에 비해 상대적으로 단순한 헤더 구조이기 때문에 오버헤드 적음
  - 실시간 전송, 신뢰성보다 속도가 중요시되는 네트워크 사용

### 29. IP(Internet Protocol) 프로토콜에 대한 설명

- IP (Internet Protocol) 설명
  - 비연결 프로토콜이다.
  - 에러 제어와 흐름제어가 없다.
  - IP 패킷이 다른 경로를 통해 전달될 수 있기 때문에 송신된 순서와 다르게 목적지에 도착할 수 있다.

```markdown
- IP 프로토콜은 신뢰성이 없는 비연결형 데이터그램 프로토콜로서 최선의 노력으로 전달을 제공하는 전송 서비스이다.
- 최선의 노력이란 IP가 오류 검사나 추적을 제공하지 않는다는 것을 의미한다.
- IP는 각기 개별적으로 전송되는 데이터그램이라는 패킷 형태로 데이터를 전송한다.
- 데이터그램은 서로 다른 경로로 전달될 수 있으므로 순서대로 도착하지 않거나 중복되어 도착할 수 있다.
- IP는 경로를 기록하지 않고, 일단 목적지에 도착한 데이터그램을 재전송하는 기능도 제공하지 않는다.
- IP 패킷에서는 헤더 체크 섬을 제공한다.
```

### 30. TCP 프로토콜에 대한 설명

- TCP 프로토콜에 대한 설명
  - 신뢰성 있는 연결 지향형 전달 서비스이다.
  - 스트림 전송 기능을 제공한다.
  - 순서 제어, 오류 제어, 흐름 제어 기능을 제공한다.
  - TCP 기본 헤더 크기는 20byte이고 60byte까지 확장할 수 있다.

### 31. TCP 프로토콜에 관련한 설명

- TCP 프로토콜에 관련한 설명
  - 흐름 제어(Flow Control)의 기능을 수행한다.
  - 전이중(Full Duplex) 방식의 양방향 가상회선을 제공한다.
  - 전송 데이터와 응답 데이터를 함께 전송할 수 있다.
- 인접한 노드 사이의 프레임 전송 및 오류 제어는 2계층인 데이터 링크 계층의 역할이고, TCP는 4계층인 전송 계층(Transport Layer)이다.

```markdown
- TCP는 전송 계층에 위치하면서 근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 일련의 옥텟을 안정적으로, 순서대로, 에러 없이 교환할 수 있게 해주는 프로토콜
- 흐름 제어(Flow Control) 기능을 활용하여 송신(송신 전송률) 및 수신(수신 처리율) 속도를 일치시킴
- 전이중(Full Duplex) 방식의 양방향 가상회선을 제공함
- 전송 데이터와 응답 데이터를 함께 전송할 수 있음
```

### 34. TCP/IP 네트워크에서 IP 주소를 MAC 주소로 변환하는 프로토콜

- `ARP`
- UDP
  - 비연결성이고, 신뢰성이 없으며, 순서화되지 않은 데이터그램 서비스를 제공하는 전송계층(4계층)의 통신 프로토콜
- ARP
  - IP 네트워크상에서 IP 주소를 MAC 주소(물리 주소)로 변환하는 프로토콜
- TCP
  - 전송 계층에 위치하면서 근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 일련의 옥텟을 안정적으로, 순서대로, 에러 없이 교환할 수 있게 해주는 프로토콜
- ICMP
  - IP 패킷을 처리할 때 발생하는 문제를 알려주는 프로토콜

### 35. UDP 헤더에 포함되는 것

- UDP 헤더 구조 (소데 랭체)
  - Source Port Number (source port address)
  - Destination Port Number
  - UDP length (UDP total length)
  - UDP Checksum (checksum)
- UDP : 데이터 전송 전에는 연결을 설정하지 않는 '비연결형' 서비스이다.
- 복구기능, 수신데이터 순서 재조정 불가

### 41. OSI 7 계층에서 단말기 사이에 오류 수정과 흐름 제어를 수행하여 신뢰성 있고 명확한 데이터를 전달하는 계층은?

- `전송 계층`

### 46. 다음 설명의 프로토콜은?

- TCP/IP 계층 구조에서 IP의 동작 과정에서의 전송 오류가 발생하는 경우에 대비해 오류 정보를 전송하는 목적으로 사용하는 프로토콜
  - ICMP

```markdown
- ARP : IP 네트워크상에서 IP 주솔르 MAC 주소(물리 주소)로 변환하는 프로토콜
- PPP : 네트워크 분야에서 두 통신 노드 간의 직접적인 연결을 위해 일반적으로 사용되는 데이터 링크 프로토콜
```

### 47. IP 주소 체계와 관련된 설명

- IP 주소 체계와 관련된 설명
  - IPv6는 주소 자동설정(Auto Configuration) 기능을 통해 손쉽게 이용자의 단말을 네트워크에 접속시킬 수 있다.
  - IPv4는 호스트 주소를 자동으로 설정하며 유니캐스트(Unicast)를 지원한다.
  - IPv4는 클래스별로 네트워크와 호스트 주소의 길이가 다르다.
  - IPv4 헤더는 20 Octet의 기본 헤더 부분과 옵션 부분으로 구성되어 있고, IPv6 헤더는 40 Octet의 고정된 길이를 가지고 있다.

### 48. IPv6에 대한 특성

- IPv6에 대한 특성
  - 2(128승)개의 주소를 표현할 수 있다.
  - 등급별, 서비스별로 패킷을 구분할 수 있어 품질 보장이 용이하다.
  - 확장기능을 통해 보안 기능을 제공한다.
  - IPv6는 16비트씩 8부분으로 나뉜 16진수로 표시한다.

|구분|IPv4|IPv6|
|:--:|--|--|
|주소길이|32bit|128bit|
|표시방법|8비트씩 4부분으로 나뉜 10진수|16비트씩 8부분으로 나뉜 16진수|
|주소 개수|약 43억 개|2(128승) = 4.3 x 10(38승)|
|QoS|Best Effort 방식(보장 곤란)|등급별, 서비스별 패킷 구분 보장|
|보안 기능|IPSec 프로토콜 별도 설치|보안과 인증 확장 헤더를 사용함으로써 인터넷 계층의 보안 기능을 강화|

### 49. 프로토콜에서 사용하는 필드와 해당 필드에 대한 설명

- 프로토콜에서 사용하는 필드와 해당 필드에 대한 설명
  - Header Length는 IP 프로토콜의 헤더 길이를 32비트 워드 단위로 표시한다.
  - Time To Live는 송신 호스트가 패킷을 전송하기 전 네트워크에서 생존할 수 있는 시간을 지정한 것이다.
  - Version Number는 IP 프로토콜의 버전 번호를 나타낸다.
- Header Length
  - IP 프로토콜의 헤더 길이를 4바이트 단위로 나타내느 필드
- Packet Length
  - IP를 포함한 패킷 전체 길이를 바이트 단위로 표시하는 필드
  - IP 패킷의 길이는 0 ~ 65535바이트
- Time To Live(TTL)
  - 송신 호스트가 패킷을 전송하기 전 네트워크에서 생존할 수 있는 시간을 표시하는 필드
  - 패킷이 각 라우터를 지나갈 때마다 1씩 감소
- Version Number
  - IP 프로토콜의 버전 번호

### 51. RIP 라우팅 프로토콜에 대한 설명

- RIP 라우팅 프로토콜에 대한 설명
  - 경로 선택 매트릭은 홉 카운트(Hop Count) 이다.
  - 최단 경로 탐색에 Bellman-Fork 알고리즘을 사용한다.
  - 각 라우터는 이웃 라우터들로부터 수신한 정보를 이용하여 라우팅 표를 갱신한다.
- IGP(Internal Gateway Routing Protocol) : RIP, OSPF
- EGP(External Gateway Routing Protocol) : BGP