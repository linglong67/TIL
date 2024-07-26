# MySQL과 Enum
## "왜 Enum 타입을 사용하는 것이 좋지 않을까?
- Enum 사용 방식보다는 참조 테이블 사용이 나을 수 있음
### 1. 정규화를 위반하는 설계
### 2. 데이터의 수정이 어려움
### 3. Enum 컬럼에 속성을 추가하거나 연관 정보를 저장할 수 없음
    참조 테이블을 사용한다면 확장성이 있어 유연한 대처 가능
### 4. 유일한 Enum 값들만 조회하는 것이 힘듦
    테이블 조회로는 실제 사용된 값이 아니면 조회할 수 없음
### 5. Enum 사용으로 얻는 최적화 효과가 그리 크지 않을 수 있음
### 6. Enum 컬럼에 정의된 값들은 다른 테이블에서 재사용할 수 없음
    반면 참조 테이블을 사용하면 다른 테이블에서 쉽게 참조 가능
### 7. Enum 컬럼을 조심해서 사용해야 함
    Enum은 내부적으로 정수 키로 참조하기 때문에 값이 아닌 인덱스를 참조하게 되는 일도 흔히 발생함
### 8. Enum은 다른 DBMS에서 널리 통용되지 않음
    표준 SQL 문법에 포함되지 않고 Enum을 지원하는 DBMS가 많지 않음