# UPSERT

- 의미상으로는 'INSERT ON CONFLICT'와 같다.
- 유일성 제약조건을 위반하지 않을 경우 INSERT, 위반할 경우 row를 업데이트

## INSERT ON CONFLICT와의 차이점은?

- UPSERT는 PK 컬럼만 고려한다. INSERT ON CONFLICT는 좀 더 유연하며 여러 다른 컬럼의 유일성을 고려하며 사용할 수 있다.
- 모든 컬럼을 inserting/updating 할 때 secondary indexes가 없을 경우, UPSERT가 첫 읽기 없이 들어가므로 INSERT ON CONFLICT보다 빠르다.
- 하나의 multi-row UPSERT가 여러개의 single-row UPSERT보다 훨씬 빠르다.
- 입력 데이터에 중복이 있을 경우 DISTINCT ON 사용
