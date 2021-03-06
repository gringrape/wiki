# Just In Time compiler
출처: https://hacks.mozilla.org/2017/02/a-crash-course-in-just-in-time-jit-compilers/

## 배경
JavaScript 는 1995 년에 만들어졌지만, 전혀 빠르게 설계되지 않았기 때문에,
10 여년동안 실제로 빠르지 않았다. 2008 년 브라우저 전쟁이 시작되면서, JIT 컴파일러를 
이용하여 JavaScript 를 컴파일하게 되면서, 10 배 이상의 속도 상승을 이루게 되었다. 

## 인터프리터 vs 컴파일러
- 인터프리터: 초기 실행이 빠르다 -> 반복적으로 해석하는 구문이 생겨서 속도가 느릴 수 있다.
- 컴파일러: 초기 실행이 느리다 -> 미리 반복구간을 해석하기 때문에 속도가 더 빠를 수 있다.

## JIT
JIT 는 이 둘의 장점만을 취하고자 한것으로, 브라우저마다 구현은 다르지만,
기본 아이디어는 `Monitor` 이다.

### Monitor - 반복되는 코드라인 검사
기본적으로 JIT 는 인터프리터 형식이다. 라인별로 해석하다가 반복적으로 해석되는
부분이 `Monitor` 에 의해 기록된다. 반복 실행되는 정도에 따라, `warm`, `hot`으로 구분된다. 
`Baseline Compiler` 로 넘겨지게 된다.

### Baseline Compiler - WARM~
`Baseline Compiler` 에서는 반복실행되는 구문을 `stub` 이라는 형태로 컴파일 한다. 
`stub` 은 타입과 라인넘버로 구분된다. 만약 같은 타입(변수 등)이 오면 
컴파일러는 해당 라인을 해석하는 대신에, 해당 타입으로 컴파일된 `stub` 을 돌려주게 되어서 속도가 향상된다.   

### Optimization Compiler - HOT!!!!
만약 어떤 라인의 반복해석 횟수가 너무 많아서, `Monitor`에 의해 `hot` 으로 분류되었다면,
해석을 하기 전에 추가적인 최적화를 고려해주는 것이 합리적이다. 이 경우, 추가적인 최적화를 담당하는 것이
`Optimization Compiler`이다.

`stub` 은 타입에 따라 다르게 생성된다. 자바스크립트는 동적 언어이기 때문에, 
변수의 타입이 정해져있지 않다. 따라서 `Baseline compiler` 에서는 하나의 라인이 여러개의 `stub`으로 컴파일 되게 된다.

만약, 하나의 타입이 온다고 '가정' 할 수 있다면, `stub`의 개수를 줄일 수 있을 것이고, 추가적인 
최적화를 기대할 수 있을 것이다. 이처럼, `Optimization Compiler` 에서는 추가적인 가정을 이용해서
속도 상승을 수행한다. 

위처럼 타입에 관한 가정을 통해 속도를 상승시키는 최적화를 `Type Specialization` 이라고 한다. 