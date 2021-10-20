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

### 프래그먼트
객체 타입에서 동일한 필드를 여러번 가져올때, 
공통되는 필드를 묶어서 반복적인 서술을 피할 수 있다.

다음 쿼리에서 Lift 정보에 관하여,
중복된 필드를 표시해보자. 

```graphql
query {
  Lift(id: "jazz-cat") {
    name  //
    status //
    capacity //
    night //
    elevationGain //
    trailAccess {
      name
      difficulty
    }
  }
  Trail(id: "river-run") {
    name
    difficulty
    accessedByLifts {
      name //
      status //
      capacity //
      night //
      elevationGain //
    }
  }
}
```

중복된 필드를 프래그먼트 단위로 묶어보자.

```graphql
fragment liftInfo on Lift {

}

query {
  Lift(id: "jazz-cat") {
    name  #
    status #
    capacity #
    night #
    elevationGain #
    trailAccess {
      name
      difficulty
    }
  }
  Trail(id: "river-run") {
    name
    difficulty
    accessedByLifts {
      name #
      status #
      capacity #
      night #
      elevationGain #
    }
  }
}
```

다음과 같이 trail 에 대한 정보를 한 번더 추출할 수 있다. 

```graphql
fragment liftInfo on Lift {
  name
  status
  capacity
  night
  elevationGain
}

fragment trailInfo on Trail {
  name
  difficulty
}

query {
  Lift(id: "jazz-cat") {
    ...liftInfo
    trailAccess {
      ...trailInfo
    }
  }
  Trail(id: "river-run") {
		...trailInfo
    accessedByLifts {
      ...liftInfo
    }
  }
}
```

### 유니온 타입
두 개 이상의 객체 타입을 섞어서 배열로 반환할 수 있다.
이 경우, 인라인 프래그먼트를 활용해서, 어떤 필드를 가져올지 
선택 할 수 있다.

## 뮤테이션

## 서브스크립션
특정 객체의 셀렉션 세트를 구독하고 있는 경우, 
서버에서는 해당 세트가 변하면 클라이언트로의 푸시가 일어나서,
값이 전달되게 된다. 

## 공통 어휘
- Definition
  = Fragment defintion
  - Query definition
- selection set  
