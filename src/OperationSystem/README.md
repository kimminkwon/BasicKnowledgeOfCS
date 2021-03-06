# Operation System

## 1. 프로세스 관리
### 1-1. 프로세스와 스레드
* 프로세스: 실행중인 프로그램, 비동기적 행위, 프로그램이 실행을 위해 메모리에 적재되면 프로세스가 된다.
    * PCB: 프로세스마다 고유로 갖는 제어 블록, 프로세스를 관리한다.
    * 프로세스 상태 전이: `생성` -> `준비` -> `실행` -> `종료`, 이 외에 실행 과정에 이벤트나 입출력이 발생하면 `대기` 상태로 전환되고, 해당 이슈 해결 후 `준비`상태로 전환된다.
* 스레드: 프로세스 내의 작업 단위
    * 단일-다중 스레드: 1개 프로세스에 1개 이상의 스레드가 존재하는가?
    * 사용자 수준-커널 수준 스레드: 스레드가 `사용자가 만든 라이브러리`와 `OS 커널` 중 어떤 것을 사용하는가? (구현 난이도와 성능 차이 존재)
    * 왜 사용하는가: 스레드로 인해 `병행성`이 증진 -> `처리율`이 높아지고, `기억 장소의 낭비`가 줄어든다.
  
### 1-2. 병행 프로세스와 상호배제
* 병행 프로세스: 1개 프로세서에서 프로세스를 빠르게 전환하여 마치 여러 개 프로세스가 동시에 실행되는 것과 같은 방법
* 상호배제: 프로세스 하나가 공유 자원을 사용중일 때, 해당 공유 자원에 다른 프로세스의 접근을 막는 것
    * `임계 영역`을 사용한다.
    * `데커`, `Test And Set`, `세마포어` 등의 상호배제 알고리즘이 존재
    * 세마포어: 하나의 변수를 부르는 명칭, 현재 CPU에서 가용한 자원의 개수를 갖는다. 이를 통해 세마포어의 값으로 접근 가능 여부를 확인 가능
  
### 1-3. 교착상태와 기아상태
* 교착상태: 프로세스가 절대로 일어나지 않을 사건을 기다리는 상태
    * 교착상태의 4가지 조건 1) `상호배제` 2) `점유와 대기` 3) `비선점` 4) `순환대기`
* 기아상태: 프로세스가 절대 사용할 수 없는 자원을 기다리는 상태   
  
### 1-4. 프로세스 스케줄링
* 스케줄링: 프로세스가 생성, 실행될 때 필요한 자원을 해당 프로세스에게 할당하는 기능
    * 장기, 중기, 단기 스케줄링
        * 장기 스케줄링: 실행할 프로세스를 준비 큐로 보낸다, 즉 `메모리`와 `디스크` 사이의 스케줄링
        * 중기 스케줄링: 준비 큐에서 프로세서와 자원을 할당할 프로세스를 선택한다, 즉 `메모리`에 너무 많은 프로세스가 올라가는 것을 방지하는 역할
        * 단기 스케줄링: 프로세서와 자원을 할당할 규칙을 정한다, 즉 `CPU`와 `메모리` 사이의 스케줄링
    * 선점, 비선점 스케줄링: 우선순위가 더 높은 프로세스가 들어왔을 때, 현재 실행 중인 프로세스를 뺏을 수 있는지(`Context Swithing`) 여부로 구분
    * 스케줄링 알고리즘
        * FIFO(First In First Out): 들어오는 순서대로 프로세스를 배치
        * SJF(Shortest Job First): 실행시간이 짧은 프로세스가 우선
        * 우선순위 스케줄링: 프로세스마다 우선순위가 존재하여 우선순위가 높은 순으로 프로세스를 배치(선점, 비선점 전부 가능)         
        * RR(Round Robin): 시분할 시스템을 위해 설계, `FIFO` + 규정시간을 넘기면 현재 실행중인 프로세스를 맨 마지막으로 배치
        * HRN(Highest Response-ratio Next): `SJF`의 개선, 프로세스의 대기시간을 우선순위에 반영한다.
  
## 2. 메모리 관리
### 2-1. 배치 전략
* Best Fit: 현재 빈 영역 중 가장 `내부 단편화가 적은 곳`에 프로세스를 배치
* Worst Fit: 현재 빈 영역 중 가장 `내부 단편화가 많은 곳`에 프로세스를 배치 
* First Fit: 프로세스가 배치될 수 있는 영역 중 가장 첫번째 영역에 배치
  
### 2-2. 연속 메모리 할당
* 연속 메모리 할당: 하나의 프로세스 내 여러개의 작업을 연속적으로 할당한다.
* 단일 프로그래밍 환경: 한번에 프로그램 하나만 사용 가능, 메모리보다 큰 프로그램 실행 불가능
* 다중 프로그래밍 환경
    * 고정 분할 방법: 메모리를 여러개의 고정된 크기로 분할하고 각 메모리마다 하나의 작업을 실행 가능 
        * n개의 공간이 각각 k의 size로 분할 됐을 때, k-10만큼의 프로세스가 어떤 공간에 할당된다면, 해당 공간에는 10만큼의 `내부 단편화`가 발생한다. 
    * 가변 분할 방법: 고정된 경계를 없애고 각 프로세스가 필요한만큼 메모리를 할당, 따라서 작업이 끝나는 순에 따라 메모리 상에 서로다른 크기의 빈공간이 생성된다. 이때 `배치전략`이 사용된다.
        * 이 때, 프로세스가 필요한만큼 메모리를 할당하므로 `내부 단편화`는 없다.
        * 단, 메모리 전체에서 작업이 빈공간에 배치되면서 작업이 할당되지 않는 낭비 공간이 생긴다. 이를 `외부 단편화`라고 한다.
* 단편화: 고정되어 분할된 한 sub 메모리에서 빈 공간은 `내부단편화`, 가변분할과 같이 전체 메모리의 시점에서 빈 공간은 `외부 단편화`라고 한다.
    * 내부단편화: 분할된 메모리 공간이 100일 때, 98짜리 프로세스를 할당하면 2만큼 공간이 남는다.
    * 외부단편화: 가변 분할 시, 서로다른 크기의 작업이 배치되며 메모리 상에 서로다른 크기의 빈공간을 만든다. 해당 빈 공간이 외부단편화이다.
  
### 2-3. 분산 메모리 할당
* 분산 메모리 할당: 하나의 프로세스 내 여러개의 작업을 분산하여 할당한다.
* 페이징: 작업을 크기가 동일한 `페이지`로 나눠, 기억 장치의 `페이지 프레임`에 분할 적재해 처리하는 방법
    * 페이지: 프로그램을 일정한 크기로 나눈 단위
    * 페이지 프레임: 주 기억장치를 페이지 크기로 나눈 단위
    * 이때, 작업을 페이지로 나누면 마지막 페이지 내에는 페이지 크기보다 작은 사이즈가 할당된다. 해당 페이지가 `페이지 프레임`에 적재되면 페이지 프레임 내부에 `내부 단편화`가 발생한다.
* 세그먼테이션: 작업을 서로다른 크기의 세그먼트로 나눠, 기억장치에 분할 적재해 처리하는 방법
    * 이때, 세그먼트의 크기가 전부 다르므로 기억장치에 남은 공간이 존재할 수 있다. 따라서 `외부 단편화`가 발생한다.
  
### 2-4. 가상기억장치 관리
* 페이지 크기에 따른 변화
    * 페이지 크기가 작을 경우: `내부 단편화` 감소, 1개 페이지 주기억장치 적재 시간 감소, `페이지 맵 테이블` 크기 증가, 입출력 시간 증가
    * 페이지 크기가 클 경우: `내부 단편화` 증가, 1개 페이지 주기억장치 적재 시간 증가, `페이지 맵 테이블` 크기 감소, 입출력 시간 감소
* 지역성(Locality): 해당 정보를 사용하여 주 기억장치로 가져오는 `워킹 셋(페이지 집합)`을 설정한다.
    * 시간 지역성: 하나의 페이지를 일정시간동안 집중적으로 액세스한다.
    * 공간 지역성: 하나의 페이지를 액세스하면, 그 근처 페이지에 액세스할 확률이 높다.
  
### 2-5. 페이지 교체 알고리즘
* 페이지 교체 알고리즘: 주 기억장치에 페이지가 가득 차있을 때 새로운 페이지가 필요하다면, 어떤 페이지를 대치시킬 것인가?
* FIFO: 가장 먼저 들어왔던 페이지를 대치시킨다.
* OPT(OPTimal replacement, 최적 페이지 대치): 앞으로 가장 오랫동안 사용하지 않을 페이지를 대치한다. 이는 페이지의 사용 스케줄을 정확히 알고 있어야해서 쉽지 않다.
* LRU(Least Recently Used, 최근 최소 사용 대치): 대치 시점에서 참조횟수가 가장 적은 페이지로 대치한다.