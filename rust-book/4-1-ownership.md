## 글 목차
### why?
- 메모리 관리
  - 메모리 영역 - stack, heap
  - 두 영역에 할당되는 값의 차이

### what?
- ownership 의 의미
- ownership rules
- *scope

### how?
- String type 의 할당
- Move
- Copy
- Clone

### Function and ownership

--------------------------

## 왜 쓸까요?
Ownership 은 Rust 의 독특한 메모리 관리 방식입니다. Ownership 을 왜 사용하는지 이해하기 위해서는, 
메모리의 구조와 메모리 관리에 대한 전반적인 지식이 필요합니다.

모든 프로그램은 작동 중에 사용하는 메모리를 관리해야 합니다. 메모리 관리란, 필요한 경우에 메모리를 사용을 요청하고
더 이상 필요하지 않은 경우에 반환하는 것을 뜻합니다. 메모리 관리에는 다양한 방법이 있습니다. 많은 언어에서는 
가비지 컬렉션이라고 하는 관리 방법을 사용합니다. 여기서 가비지란 더이상 사용되지 않은 메모리 영역을 뜻합니다.
가비지 컬렉터는 지속적으로 가비지가 있는지 검사하고, 해당 메모리를 다시 활용할 수 있도록 만들어 주는 역할을
하게 됩니다.

이때 메모리 할당과 해제가 일어나는 메모리 영역을 heap 영역이라고 부릅니다. 다른 영역은 stack 영역이 있는데,
heap 영역과 stack 영역은 저장되는 데이터 종류의 차이가 생깁니다. 

### stack
- stack 영역은 자료구조 stack 의 거동과 동일 LIFO
- 고정된 크기를 가진 데이터만 저장 가능.

### heap
- stack 보다 훨씬 덜 구조화된 영역
- allocation 이라고 부르는 프로세스를 통해 메모리 사용

> - 사용 가능한 빈 공간을 찾음
- 해당 부분을 사용중으로 표시
- 해당 부분을 가리키는 포인터 반환

### stack vs heap
> 데이터에 엑세스하는 속도는 stack 의 경우가 더 빠르다.
- heap 의 경우, 포인터를 통해 데이터에 접근해야함. 
- stack 은 단순히 pop 을 통해 다음 데이터에 접근 가능.
- 포인터를 통해 데이터를 이곳저곳 건너뛰는 비용때문에 흔히 더 느림.

ownership 의 목표는 heap 영역의 데이터를 관리하는 것.
어떤 값이 heap 에 해당하는지 판단하고, 중복된 데이터를 막고,
사용하지 않는 데이터를 제거해 해당 영역을 다시 사용할 수 있도록 만드는 것.

## Ownership 이란?
Ownership 은 Ownership 이 갖는 규칙을 통해 이해할 수 있습니다.

> - Rust 의 모든 값은 owner 라고 하는 변수를 갖는다.
- 특정 시점에는 하나의 owner 만 존재할 수 있다.
- owner 가 scope 를 벗어나면 값은 drop 된다.

여기서, owner 라는 변수가 값을 소유하게 된다는 특징과,
owner 가 scope 를 벗어나면 자동으로 메모리에서 해제하게 된다는
특징이 메모리 안전성을 만들어 냅니다.

heap 영역에 할당되는 String 타입의 값을 통해서, ownership 규칙을
상세하게 알아보겠습니다.

## 참고 자료
- 메모리 관리: https://en.wikipedia.org/wiki/Memory_management