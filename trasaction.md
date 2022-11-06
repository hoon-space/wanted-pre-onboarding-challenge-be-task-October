
# 트랜잭션(Transaction)

여러 쿼리를 하나의 논리적인 기능을 수행하기 위한 작업의 단위 <br>
또한, 트랜잭션 내 작업이 커밋과 롤백을 통해 데이터의 무결성을 보장할 수 있습니다.


## 트랜잭션 성질

### ACID
트랜잭션이 안전하게 수행되는 보장하기 위한 성질

- **Atomicity(원자성) - All or Noting** <br>
  트랜잭션 작업 후 일련의 데이터들이 커밋을 통해 전부 반영되던지, 아니면 롤백되어 전부 반영되지 않던지를 나타내며 데이터 무결성을 고려하는 특징
- **Consistency(일관성)** <br>
  DB의 데이터는 '허용된 방식'으로 데이터를 변경해야 함으로 DB 제약조건에 위반할 경우 트랜잭션을 종료한다. 일관성을 유지해야 한다.
- **Isolation(독립성, 격리성)** <br>
  각각의 트랜잭션은 서로 간섭없이 독립적으로 이루어져야 한다.
- **Durability(지속성)** <br>
  트랜잭션이 성공적으로 완료되었으면 결과는 영구히 반영되어야 한다.

  
## 트랜잭션 전파

트랜잭션 범위는 **_커넥션 단위_** 로 수행된다.<br>
여러 메서드 호출이 한 트랜잭션으로 묶이도록 하기 위해 필요 <br>
롤백해야 하는 범위

![트랜잭션_범위_커넥션](https://user-images.githubusercontent.com/59961350/195955775-269c6933-dbf8-4b33-ae99-e9b057d3ce9a.jpg)



- 스프링 프레임워크에서 지원하는 트랜잭션 처리(전파)
  - @Transaction <br>
    메서드 간 커넥션 객체를 전달하지 않아도 한 트랜잭션으로 묶여서 실행



### 트랜잭션 격리수준

데이터베이스 같은 데이터에 동시에 접근함에 따라 트랜잭션 격리 수준 구분 

왜? 트랜잭션이 순차적으로 실행되면 격리성은 높아지지만, 동시성은 낮아져 성능이 안좋아지기 때문에 
격리성과 동시성은 반비례 관계입니다. 

1. READ_UNCOMMITTED
   - dirty read, non-repeatable read, phantom read
2. READ_COMMITTED
   - non-repeatable read, phantom read
3. REPEATABLE_READ
   - phantom read
4. SERIALIZABLE(순차적, 간섭 X)


- phantom read <br>
  한 트랜잭션 내에서 동일한 쿼리를 2번 이상 보냈을 때, 조회 결과가 다름(ex. 행이 추가됨, 데이터 업데이트)


- non-repeatable read <br>
  한 트랜잭션 내에서 같은 행을 2번 이상 조회를 하였을 때, 그 값이 다름(ex. 행내 값이 다름)


- dirty read <br>
  하나의 트랜잭션이 다른 트랜잭션의 커밋되지 않은 데이터를 읽는 현상





### 참고

https://www.youtube.com/watch?v=urpF7jwVNWs

