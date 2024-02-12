# 정보처리기사 2024

## # 2-3. 소프트웨어 개발 - 제품 소프트웨어 패키징

### # 1. 제품 소프트웨어 패키징 2-50page

### 1. 소프트웨어 패키징에 대한 설명

- 소프트웨어 패키징에 대한 설명
  - 신규 및 변경 개발 소스를 식별하고, 이를 모듈화하여 상용제품으로 패키징한다.
  - 고객의 편의성을 위해 매뉴얼 및 버전 관리를 지속적으로 한다.
  - 범용 환경에서 사용이 가능하도록 일반적인 배포 형태로 패키징이 진행된다.
  - 소프트웨어 패키징은 사용자 중심으로 진행된다. (개발자 중심 x)

### 3. 디지털 저작권 관리(DRM)의 기술 요소

- 디지털 저작권 관리(DRM)의 기술 요소 (암키식저 파정크인)
  - 암호화
  - 키 관리
  - 식별 기술
  - 저작권 표현
  - 암호화 파일 생성
  - 정책 관리
  - 크랙 방지
  - 인증
- 방화벽 기술 (x)

### 7. 디지털 저작권 관리(DRM)의 구성 요소

- 디지털 저작권 관리(DRM)의 기술 요소 (제소분 클콘패컨보)
  - 콘텐츠 제공자(Contents Provider)
  - 콘텐츠 소비자(Contents Customer)
  - 콘텐츠 분배자(Contents Distributor)
  - 클리어링 하우스(Clearing House)
  - DRM 콘텐츠(DRM Contents)
  - 패키저(Packager)
  - DRM 컨트롤러(DRM Controller)
  - 보안 컨테이너(Security Container)

### 9. 디지털 저작권 관리(DRM) 기술

- DRM 기술요소 (암키식저 파정크인)
  - 암호화
  - 키 관리
  - 식별 기술
  - 저작권 표현
  - 암호화 파일 생성
  - 정책 관리
  - 크랙 방지
  - 인증

---

### # 2. 제품 소프트웨어 매뉴얼 작성 2-63page

### 3. 소프트웨어 설치 매뉴얼 포함될 항목

- 제품 소프트웨어 설치 매뉴얼 구성요소 (개파절아 삭버고준)
  - 제품 소프트웨어 개요
  - 설치 관련 파일
  - 설치 절차
  - 설치 아이콘
  - 삭제 방법
  - 설치 버전 및 작성자
  - 고객 지원 방법 및 FAQ
  - 준수 정보 & 제한 보증

### 7. 다음에 해당하는 용어는?

- 소프트웨어 품질 목표 중 주어진 시간동안 주어진 기능을 오류 없이 수행하는 정도를 나타내는 것은?
  - 신뢰성

```markdown
- ISO/IEC 9126의 소프트웨어 품질 특성 중 신뢰성(Reliability)은 명세된 조건에서 사용될 때 성능 수준을 유지할 수 있는 소프트웨어 제품의 능력이다.
- 신뢰성은 옳고 일관된 결과를 얻기 위하여 요구된 기능을 수행할 수 있는 정도이고, 주어진 시간 동안 주어진 기능을 오류 없이 수행하는 정도이다.
```

### 10. 다음에 해당하는 법칙은?

- S/W Project 일정이 지연된다고 해서 Project 말이에 새로운 인원을 추가 투입하면 Project는 더욱 지연되게 된다는 내용과 관련되는 법칙은?
  - `Brooks의 법칙`

### 17. 소프트웨어 품질 관련 국제 표준인 ISO/IEC 25000에 관한 설명

- 소프트웨어 품질 관련 국제 표준인 ISO/IEC 25000에 관한 설명
  - 소프트웨어 품질평가를 위한 소프트웨어 품질평가 통합모델 표준이다.
  - System and Software Quality Requirements and Evaluation으로 줄여서 SQuaRE라고도 한다.
  - 기존 소프트웨어 품질평가 모델과 소프트웨어 평가 절차 모델인 ISO/IEC 9126과 ISO/IEC 14598을 통합하였다.

```markdown
- ISO/IEC 25000는 기존 소프트웨어 품질평가 모델과 소프트웨어 평가 절차 모델인 ISO/IEC 9126과 ISO/IEC 14598을 통합한 소프트웨어 품질 평가 모델 국제 표준으로 SQuaRE(System and Software Quality Requirements and Evaluation)라고 한다.
- ISO/IEC 2502n에서 소프트웨어의 내부 측정, 외부 측정, 사용 품질 측정, 품질 측정 요소 등을 다룬다.
```

---

### # 3. 제품 소프트웨어 버전 관리 2-72page

### 2. 제품 소프트웨어의 형상 관리 역할

- 제품 소프트웨어의 형상 관리 역할
  - 형상 관리를 통해 이전 리비전이나 버전에 대한 정보에 접근 가능하여 배포본 관리에 유용
  - 불필요한 사용자의 소스 수정 제한
  - 동일한 프로젝트에 대해 여러 개발자 동시개발 가능

```markdown
- 제품 소프트웨어의 형상 관리 역할은 버전에 대한 쉬운 정보 접근성이 있고, 불필요한 사용자에 대한 접근 제어 역할이 있고, 동일 프로젝트에 대한 동시 사용성이 있고, 빠른 오류 복구가 있다.
- 형상 관리와 버전 관리를 통해서 프로젝트의 비용을 관리하지 않는다.
```

### 3. 다음에 해당하는 버전 관리 도구는?

- 동시에 소스를 수정하는 것을 방지하며 다른 방향으로 진행된 개발 결과를 합치거나 변경 내용을 추적할 수 있는 소프트웨어 버전 관리 도구는?
  - `RCS(Revision Control System)`

```markdown
- RCS는 CVS(Concurrent Version System)와 달리 소스 파일의 수정을 한 사람만으로 제한하여 다수의 사람 이 파일의 수정을 동시에 할 수 없도록 파일 잠금 방식으로 버전을 관리 하는 도구이다.
- RCS는 다른 방향으로 진행된 개발 결과를 합치거나 변경 내용을 추적할 수 있는 소프트웨어 버전 관리 도구이다.
```