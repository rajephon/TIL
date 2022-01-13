## Index-Only Scan: 테이블 엑세스 피하기

- 인덱스가 테이블 엑세스를 방지하는경우(예를 들어, select 컬럼과 where 조건 모두 포함하는 인덱스) covering index라고 부르기도한다.
- 그러나 인덱스의 속성처럼 들림. index-only scan이 훨씬 실행 계획 최적화임을 잘 나타냄.
- 인덱스에는 이미 원하는 컬럼의 복사본이 있을 경우, 테이블엑세스를 할 필요가 없다.
- 인덱스가 걸리지 않은 컬럼을 작더라도 활용하는 순간, 테이블엑세스가 발생한다. 인덱스가 걸려있는 컬럼만 활용하거나, 별도의 서브쿼리 활용.

- `select *`를 피하고, 필요한 컬럼만 가져온다.


### Reference
- [Index-Only Scan: Avoiding Table Access](https://use-the-index-luke.com/sql/clustering/index-only-scan-covering-index)