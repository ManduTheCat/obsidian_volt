오라클 기준 둘은 같은 dml 이지만 같은 데이터를 넣는데 성능차이가 날수 있다.


우선 insert 의 성능에 영향주는 요소  delete 의 성능에 영향주는 욧 비교해보자

### INSERT

* 로그 기록 (redo.rlog)
	* LOG AHEAD 기법으로 인해 항상 리두 로그를 기록하고 디스크에 기록한다.
	* 로그 기록하는 프로세스가 속도에 영향을 준다.
	* 데이터 겟수만큼 리두 로그가 일어난다.
	* insert 는 다이렉트 로딩 힌트를 사용해 데이터를 저장해 성능을 확보할수 있다.
	
* HWM BUMP UP
	* 데이터를 INSERT 테이블내 논리적 저장단위인 블록 을 새롭게 확보해야하는데
	  이때 HWM 기준으로 블록의 더 하위 저장단위인  EXTNT 가 저장되기 떄문에 HWM 가 이동한다 (뒤로) HWM 이동하는 작업은 고비용작업이기 때문에 성능에 영향을 주게 된다. 
	* 즉 HWM 이 후진 해야 데이터 저장이 가능해진다.
       * 이 모든게 데이터 겟수만큼 일어난다. 한번에 많이한만큼 성능저하
       
       
* 인덱스 갯수
	* 인덱스가 이전에 존재 하고 있다면 인덱스를 추가하는 작업이진행된다.
	* 데이터 겟수만큼 인덱스 추가작업이 일어난다.
	* 인덱스는 순서를 유지해야하기 때문에 고비용의 작업이 일어난다.
* 롤백을 위한 로그기록 (undo.log)
	* 커밋의 ROLL BACK  수행할때 사용하는 undo.log 를 갱신하는 작업이 데이터 갯수만큼 일어난다
	* 변경전 데이터를 기록하는 방식으로 동작한다.
* 디스크 I/O
	* HWP BUMP UP 을 제외한 작업은 모두 디스크에서 일어난다.

### DELETE
	* HWM BUMP UP 를 제외하고 인서트와 동일하다.



## 성능은INSERT 보다 DELETE 가 더느리다
* 분명 성능에 영향을 주는 요소는 DELTE  가 더 적지만 동일한 데이터양에 대해선 DELETE 가 더느리다.
* undo 를 진행하면서 이전데이터를 정보가 있냐 없냐 차이가 있기 떄문에 delete 가 더느림.
* undo 는 디스크 IO 기 떄문에 더느리다.


## 추가 질문
* update 와 delete 중 누가더 느릴까?
* 성능이 느린 delete 를 어떻게 하면 빠르게 할수 있을까?


###참조
* dml 의 성능 고찰
* http://www.gurubee.net/lecture/2283 
* delete 가 더 비용을 발생시키다.
* http://www.gurubee.net/lecture/2283
* delete 와 update 성능 최적화
* https://dataonair.or.kr/db-tech-reference/d-story/data-story/?mod=document&uid=62944