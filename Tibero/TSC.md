tibeor active stanby   간 replication 으 로 이중화 하는 방법

## observer mode

observer 계정을 을통해 옵져브 모드로 동작한다.
cm 을 사용해서 자동 active stanby 간 replication 을 통해 데이터 파일을 공유한다.

## non-observer mode

백업을 수동으로 해야하는 방법 즉 , 자동으로 replication 이 일어나지 않는다.

### switch over
pirmary -> standby 
standvy -> primary


### stand by 에서 테이블 조회를 테스트

다음을 수행해 리커버리 모드를 read only로 바꿔줘야 확인할수 있다
```sql
alter database open read only continue recovery;

```

이후 다시 리커버리 모드로 만들어줘야한다

```sql
alter database standby;

```
