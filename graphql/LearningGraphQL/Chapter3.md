# GraphQL 쿼리어
실습: http://snowtooth.moonhighway.com/

### 쿼리 
```graphql
query {
  allLifts {
    name
    status
  }
}
```

### 여러 요청 조합
```graphql
query {
  liftCount(status: OPEN)

  allLifts {
    name
    status
  }
  
  allTrails {
    name
    difficulty
  }
}
```

### 용어
- query, mutation 타입
작업의 진입점을 의미하는 타입. 루트 타입이라고도 함.
https://graphql.org/learn/schema/#the-query-and-mutation-types
- selection set
블록으로 감싸진 필드들

### 별칭
```graphql
query liftsAndTrails {
  open: liftCount(status: OPEN)
  
  myLifst: allLifts {
    name
    status
  }
  
  myTrails: allTrails {
    name
    difficulty
  }
}
```

### 필터링
필드에 인수를 넣어서 필터링을 할 수 있다
```graphql
query liftsAndTrails {  
  myLifst: allLifts(status: CLOSED) {
    name
    status
  }
}
```

### 타입
graphql 에서 필드의 타입은 `스칼라` 타입과 `객체` 타입으로 나눌 수 있다. 

스칼라 타입은 다른 언어에서는 원시 타입이라고 부르는 것과 유사. 트리의 leaf 역할을 한다. 

객체 타입은 다른 필드를 묶어주는 역할을 한다. 중첩을 통해서 서로 다른 객체를 연결(엣지) 한다. 

```graphql
query liftAccessedByJazzCat {
  Lift(id: "jazz-cat") {
    capacity
    trailAccess {
      name
      difficulty
    }
  }
}
```