# 기술스택
### Node.js 기반 프레임워크
Express기반
### Typescript
### 데이터베이스(MySQL 8.x)
### ORM(TpyeORM)
### REST API
# Node.js
> 단일 쓰레드에서 구동되는 non-bloacking I/O 이벤트 기반 비동기 방식

- 단일 쓰레드 이벤트 기반 비동기 방식으 서버의 자원에 크게 부하를 주지 않음
- 하나의 쓰레드에 문제가 생기게 되면 애플리케이션 전체가 오류를 일으킬 위험이 있음
- 이벤트 기반 비동기 방식으로 복잡한 기능을 구현하다 보면 여러 이벤트를 동시에 처리하는 경우 콜백 지옥에 빠질수 있음
## 이벤트 루프
> 시스템 커널에서 가능한 작업이 있다면 그 작업을 커널에 이관함

6개의 단계
![](https://velog.velcdn.com/images/chch4lee1/post/c2060643-084f-4ee6-871e-2eae57a5f337/image.PNG)

- idle & prepare단계를 제외한 어느 단계에서나 실행 가능
- nexTickqueue,microTaskQueue는 이벤트 루프의 구성요소는 아니고 큐에 들어 있는 작업 역시 이벤트 루파가 어느 단계에 있는지 실행 가능
- node main.js 명령어로 Node.js 애플리케이션을 콘솔에서 실행하면 먼저 이벤트 루프를 생성 -> 메인 모듈인 main.js 실행
- 만약 큐가 모두 비어서 더 이상 수행할 작업이 없으면 루프를 빠져나가 프로세스를 종료
#### Timer 단계
- 큐에는 **setTimeout** or **setInterval**과 같은 함수를 통해 만들어진 타이머들을 큐에 넣고 실행
#### Pending(i/o) 콜백 단계
- 큐에 들어있는 콜백들은 현재 돌고 있는 루프 이전의 작업에서 큐에 들어온 콜백
- Timer 단계를 거쳐 pending 콜백 단계에 들어오면 이전 작업들의 콜백이 pending_queue에서 대기중인지 확인
- 만약 실행 대기 중이면 시스템 실행 한도에 도달할 때까지 꺼내어 실행
#### Idle, Prepare 단계
- 매 틱(Tick, 매 단계가 이동하는 것)마다 실행됨
#### Poll 단계
> 이벤트 루프 중 가장 중요한 단계

- 새로운 I/O이벤트를 가져와서 관련 콜백을 수행
- poll 큐에 쌓인 콜백 함수들을한도가 넘지 않을때까지 모두 동기적으로 실행
- 한도가 넘거나, 더이상 실행할 콜백함수가 없을때는 별도의 규칙에 따라 다음 단계로 넘어가거나 대기함

**메인기능**
1. IO를 위해 block하고 poll해야하는 시간을 계산
2. poll 큐에 이벤트를 생성

스케줄된 timer가 없는경우
- 만약 poll 큐가 차있는 경우
   - 이벤트 루프는 큐를 돌면서 콜백을 동기적으로 실행
   - 큐를 모두 비우거나 실행 제한 횟수까지 돌릴 때까지
- poll 큐가 비어있는 경우
   - 스크립트가 setImmediate()에 의해 예약되어있는 경우
     - 이벤트 루프는 poll 단계를 나와 check 단계로 진입해 명령을 실행
   - setImmediate() 명령이 없는 경우
     - 이벤트 루프는 poll 큐에 콜백이 추가되기를 기다렸다가 바로 콜백을 실행
#### check 단계
- setImmediate의 콜백만을 위한 단계
- 큐가 비거나 시스템 실행 한도에 도달할 때까지 콜백을 수행
#### close 단계
- socket.n('close', () => {})과 같은 close나 destory 이벤트 타입의 콜백이 여기서 처리됨
- 이벤트 루프는 close 콜백 단계를 마치고 나면 다음 루프에서 처리해야 하는 작업이 남아 있는지 검사
- 만약 작업이 남아 있다면 Timer 단계부터 한번 더 루프를 돌게 되고 아니라면 루프를 종료
#### nextTickQueue과 microTaskQueue
1. nextTickQueue는 process.nextTick() API의 콜백들을 가지고 있음
2. microTaskQueue는 Resolve된 Promise의 콜백을 가지고 있음
- 우선 순위는 nextTickQueue가 더 높음










#### 참고자료
https://velog.io/@adam2/Node.js-%ED%95%B4%EB%B6%80%ED%95%99-2-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-phase
https://wikidocs.net/158475
