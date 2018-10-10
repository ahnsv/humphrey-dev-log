---
title: 자바스크립트 개발자를 위한 함수형 프로그래밍 - 1
images: 'images/functional-programmiing-for-javascript.png'
date: 2018-05-28 19:16:53
---

## Editorial
최근 지금까지 내가 쓴 코드들을 보면서 환멸을 느끼고, 정말 [클린 코드](https://www.goodreads.com/book/show/3735293-clean-code)를 쓸 수 있으면 좋겠다... 라는 생각에서 함수형 프로그래밍을 파기 시작했다. 하지만 학부 수업 시간에 쓴 프로그래밍 언어를 제외하고 개인 프로젝트에서 제일 많이 사용하기도 하고 제일 익숙한 언어가 (아쉽게도) 자바스크립트여서 함수형 프로그래밍을 해 보기 어려웠다. (최근 자바스크립트를 이용한 함수형 프로그래밍을 하는 사람들이 꽤 보이긴 하지만, 약한 타입을 갖고 있는 언어이기 때문에 함수형 프로그래밍의 장점을 모두 끌어내기는 어렵다는 게 다수의 의견으로 보였다).

때문에 한 선임에게 함수형 언어인 Haskell 책을 받아서 해 보고있었는데, 많은 사람들이 이야기 하듯 참 배우기 어려웠고 지금도 붙들고 있다. 무엇보다 아직 Haskell이라는 새로운 언어를 배우면서 함수형 프로그래밍 방법론을 같이 하는 게 여간 어려운 게 아니라고 느껴졌다. 

그래서 자바스크립트로 조금 더 함수형 프로그래밍 개념을 더 잘 익히고 싶어졌고, [Medium](https://medium.com/)에서 좋은 글을 찾아서 공유하고자 한다. 

**Disclaimer: 오역과 의역이 많을 수 있음. 아직 함수형 프로그래밍 지식이 부족해서 개념을 잘 못 이해하고 쓸 수 있음...** 

> 이 글은 [Functional Programming for JavaScript People](https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504)을 번역한 글 입니다.
> ES6에 대한 지식이 필요합니다. 

## 자바스크립트 개발자를 위한 함수형 프로그래밍

여러분들과 같이 나도 몇 달 전 함수형 프로그래밍에 대해 많이 들어봤지만 뭔지 잘 모르겠었다. 그냥 유행어 같았다.
그 이후로 부터 나는 함수형 프로그래밍을 깊게 팠고, 혼란스러워 하는 초보자들에게 도움을 줄 수 있을 거라고 생각했다. 

함수형 프로그래밍을 이야기 할 때, 보통 [Haskell](http://haskell.org)가 낫냐 [Lisp](https://en.wikipedia.org/wiki/Lisp_%28programming_language%29)냐 라는 토론들이 나온다. 사실 둘은 꽤 많이 다르고 장단점이 있다. 이 글을 읽고 난 후 함수형 프로그래밍 언어들이 무엇인지 좀 더 잘 알게 될 수 있으면 좋겠다. 두 언어 모두 다른 언어에 영향을 주었다. 그런 언어들 중에 JavaScript로 컴파일되는 [Elm](http://elm-lang,org)와 [ClojureScript](github.com/clojure/clojurescript) 있다. 각 언어들에 대해서 알아보기 전에, **핵심 개념들과 패턴들에 대해 알아보자.**

> 본격적으로 들어가기 전에 손에 커피 하나 들고 시작하는 걸 추천한다.

### 순수 함수
함수형 프로그래밍의 핵심에는 [람다 미적분학](https://en.wikipedia.org/wiki/Lambda_calculus)이 있다. 수학자들은 프로그램을 데이터의 변형으로써 설명하고자 한다. 이는 [순수 함수](https://en.wikipedia.org/wiki/Pure_function)의 개념으로 연결된다. 순수 함수는 [부작용](https://en.wikipedia.org/wiki/Side_effect_%28computer_science%29)이 없는 함수이다. 순수 함수는 오직 입력 또는 인자에만 의존하고, 같은 입력을 주었을 때 모두 같은 결과를 리턴해야 한다. 

```javascript
// 순수 함수
const add10 = (a) => a + 10
// 외부 변수로 인한 순수하지 못한 함수
let x = 10
const addx = (a) => a + x
// 부작용이 있는 순수하지 못한 함수
const setx = (v) => x = v 
```
순수하지 않은 함수는 변수 `x`에 의존한다. `x`의 값을 변경을 한다면, 함수 `addx`의 값도 달라진다. 이러한 것들은 컴파일 타임에서 분석과 최적화를 방해한다. 자바스크립트 개발자들에게 좀 더 현실적으로, 순수 함수는 프로그래밍의 인지 부하적 역할을 한다 (i.e., 즉, 프로그래밍의 직관적으로 할 수 있게 만들어 준다). 순수 함수를 쓴다면, 문제를 일으킬 여지가 있는 외부적 요인들을 신경쓰지 않고, 함수 본체에만 신경 쓰면 된다. 

### 함수 합성
순수 함수의 장점 중 하나로는 함수들을 합성해서 새로운 함수로 만들 수 있다는 것이다. 람다 미적분학에서 프로그램들을 설명하는 데 쓰이는 연산자가 바로 `compose`이다. `compose`는 두 개의 함수를 인자로 받아, 새로운 함수로 합성한다.

```javascript
const add1 = (a) => a + 1
const times2 = (a) => a * 2
const compose = (a, b) => (c) => a(b(c))
const add1OfTimes2 = compose(add1, times2)
add1OfTimes2(5) // => 11
```

`compose`는 전치사 "of"와 같다. 인자의 순서와 함수들이 어떻게 계산되었는 지 유심히 보자. `add1OfTimes2`에서 두 번째 함수가 먼저 계산되었다. `compose`는 unix를 해 본 사람이라면 친숙한 `pipe`와 정반대되는 개념이다 (`pipe`는 함수의 배열을 받는다).

```javascript
const pipe = (fns) => (x) => fns.reduce((v, f) => f(v), x)
const times2add1 = pipe([times2, add1])
times2add1(5) // => 11
```
함수 합성을 이용하면 조금 더 어려운 데이터 변형도 작은 함수들을 합성함으로써 가능하다. 더 자세하고 간결한 함수 합성에 대한 설명은 [이 글](http://fr.umio.us/why-ramda/)을 참고해라.

현실적으로 말해서, 함수 합성은 객체지향 상속의 더 나은 대안이다. 현실적인 예제를 보며 알아보자. 

```javascript
const greeting = (name) => `Hello ${name}`
```
간단한 순수 함수이다. 유저에 대한 정보를 가지고 좀 더 꾸며보자.
```javascript
const greeting = (name, male=false, female=false) =>
  `Hello ${male ? ‘Mr. ‘ : female ? ‘Ms. ‘ : ‘’} ${name}`
```
나쁘지 않은 코드다. 하지만 좀더 많은 항목들을 위해 불리언 값을 만든다면 어떨까? "Dr."나 "Sir"라든가 아님 "MD"나 "PhD"같은 것들. 

불리언들을 함수에 추가하는 것은 객체 지향의 상속과 같지 않다. 하지만, 객체가 상속되면서 프로퍼티와 매써드를 extend하고 override는 비슷하다. 그러니 불리언 옵션을 쓰기 보단, 함수 합성을 사용하도록 해 보자.

```javascript
const formalGreeting = (name) => `Hello ${name}`
const casualGreeting = (name) => `Sup ${name}`
const male = (name) => `Mr. ${name}`
const female = (name) => `Mrs. ${name}`
const doctor = (name) => `Dr. ${name}`
const phd = (name) => `${name} PhD`
const md = (name) => `${name} M.D.`

formalGreeting(male(phd("Chet"))) // => "Hello Mr. Chet PhD"
```
이게 조금 더 다루기 쉽고 이성적으로 생각하기 편하다. 각 함수는 하나의 간단한 일을 하고, 그것들을 합성하기 쉽다. 이제 pipe를 한 번 써보자.

```javascript
const identity = (x) => x
const greet = (name, options) => {
  return pipe([
    // greeting    
    options.formal ? formalGreeting :
    casualGreeting,
    // prefix
    options.doctor ? doctor :
    options.male ? male :
    options.female ? female :
    identity,
    // suffix
    options.phd ? phd :
    options.md ?md :
    identity
  ])(name)
}
```

또 다른 순수 함수와 함수 합성을 이용하는 장점은 에러를 찾기 편하다는 것이다. **에러가 생길 때 마다, 버그가 생긴 곳의 함수 스택들을 확인하면 된다. 객체 지향에서 이는 꽤 혼란스러울 수 있다. 다른 객체가 어떤 상태를 갖고 있는 지 모르기 때문이다.**

### 함수 커링

함수 커링은 하스켈을 만든 Haskell Curry로 부터 만들어 졌다. 함수 커링이란 함수가 필요한 인자보다 적은 파라미터를 인자로 받아서 나머지 인자 자리에 다른 함수를 받는 것을 말한다. 이에 대한 내용이 더욱 [잘 설명되있는 글](https://hughfdjackson.com/javascript/why-curry-helps/)이 있지만, 여기서는 Ramda.js의 커링 함수의 예제로 커링에 대해 알아보자.

밑의 예제에서 커링화 된 함수 `add`를 만들어보자. 이 함수는 두 개의 인자를 받는다. 한 인자만을 받았을 때, `add1`이라는 한 개의 인자만을 가지는 함수를 반환한다.

```javascript
const add = R.curry((a, b) => a + b)
add(1, 2) // => 3
const add1 = add(1)
add1(2) // => 3
add1(10) // => 11
```
하스켈에서 모든 함수는 커링화 되어있다. 선택적이나 기본 매개 변수가 없다.

현실적으로, 함수 커링은 `map`, `compose`, `pipe` 함수들과 같이 사용했을때 훨씬 편리하다. 

```javascript
const users = [{name: 'chet', age:25}, {name:'joe', age:24}]
R.pipe(
  R.sortBy(R.prop('age')), // sort user by the age property
  R.map(R.prop('name')),   // get each name property
  R.join(', '),            // join the names with a comma
)(users)
// => "joe, chet"
```
훨씬 데이터 프로세싱이 선언적이다. 주석을 참고해서 코드를 자세히 보자.

### 모나드(Monads)와 펑터(Functors)
모나드와 펑터는 어렵게 들리지만 사실 당신이 이미 알고 있는 것들이다. 더 자세히 모나드와 펑터에 대해서 알고 싶으면, 그림으로 쉽게 설명된 [이 글](http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html)을 읽어보는 것을 추천한다. 그렇게 복잡하지 않다. 

모나드는 굉장히 흥미롭다. 모나드는 하나의 값을 위한 컨테이너고, 컨테이너를 열고 값을 이용해 무언가 하려고 하기 위해선, 값으로 매핑을 해줘야한다. 간단한 예제를 보자.

```javascript
// monad
list = [-1,0,1]
list.map(inc) // => [0,1,2]
list.map(isZero) // => [false, true, false]
```

모나드와 펑터의 중요한 점은 수학자들이 범주론에서 연구를 해 왔다는 것이다. 범주론은 프로그램을 이해하는 틀을 제시할 뿐만 아니라, 프로그램이 컴파일 되고 코드를 분석하고 최적화할 수 있는 대수학적 정리와 증명을 제시한다. 이것은 하스켈의 장점 중 하나이다 - Glasgow Haskell 컴파일러는 인류 천재성의 산물이다. 

범주론의 수학적 정리들과 개념들을 보자.

```javscript
list.map(inc).map(isZero) // => [true, false, false]
list.map(compose(isZero, inc)) // => [true, false, false]
```

`map`이 컴파일 되면, 효율적인 while 루프를 사용한다. 전반적으로, O(n) (선형 시간) 작업이지만, 포인터를 리스트의 다음 아이템으로 가리키게 할 때 오버헤드가 생기게 된다. 그래서 두 번째 버전이 두 배 더 효율적이다. 하스켈은 컴파일 단계에서 첫 번째에서 두 번째 라인으로 바꿔준다. 때문에 실행 속도가 엄청나게 빠르게 한다. 이에 대해서는 나중에 더 자세하게 다뤄보자.

모나드에 대해서 더 알아보자면, `Maybe` 모나드라는 아주 흥미로운 모나드가 있다 (Swift에서는 Option 또는 Optional이라고도 불린다). 하스켈에서는 `null`이나 `undefined`가 존재 하지 않는다. `null`이 될 만한 것들을 표현하기 위해서는 모나드로 감싸주어서 하스켈 컴파일러가 어떻게 해야할 지 알려 줘야한다. 

`Maybe` 모나드는 `Nothing`이나 `Just something`인 [유니온 타입](https://en.wikipedia.org/wiki/Union_type)이다. 하스켈에서 `Maybe`를 이와 같이 정의한다.

```javascript
type Maybe = Nothing | Just x
```

소문자 `x`는 다른 타입을 의미한다. 모나드이기 때문에, `.map()`를 사용해 `Maybe`가 담고 있는 값을 바꿔줄 수 있다! `Maybe`를 매핑해 줄 때, `Just`타입일 때, 함수를 적용해서 다른 값을 가진 `Just`를 리턴한다. `Nothing`타입일 때, `Nothing`을 리턴한다. 하스켈의 문법은 굉장히 간단하고 [패턴 매칭](https://en.wikipedia.org/wiki/Pattern_matching)을 사용하지만, 자바스크립트에서는 `Maybe`를 이와 같이 사용한다.

```javascript
const x = Maybe.Just(10)
const n = x.map(inc)
n.isJust() // true
n.value() // 11
const x= Maybe.Nothing
const n = x.map(inc) // no error!
n.isNothing // true
```
이 모나드는 자바스크립트에서는 쓰잘데기 없어 보이지만, 하스켈에서는 왜 엄청나게 유용한지 알아볼 필요가 있다. **하스켈은 모든 극단적인 상황에서 (Maximum/Minium, If/Else 등등) 해야할 일들을 정의하지 않으면 컴파일 되지 않는다.** HTTP 요청을 보내면, `Maybe` 타입을 받는다. 요청이 실패할 수 있고, 아무것도 리턴하지 않을 수도 있기 때문이다. 요청이 실패할 경우를 핸들링하지 않으면, 컴파일되지 않는다. 당연히 런타임 에러도 나지 않는다. 아마 코드가 제대로 작동하지 않을 것이지만, 자바스크립트 처럼 마법(?)같이 멈추지는 않을 것이다. 

> 이것은 Elm의 장점 중 하나이다. 타입 시스템과 컴파일러는 프로그램이 런타임 에러가 발생하지 않고 실행되게 만든다.

모나드와 대수학적 관점에서 코드를 생각해 보는 것은 문제를 체계적으로 정의하고 이해하게 도와준다. 예를 들어, `Maybe`의 흥미로은 확장으로는 [ROP(Railway-Oriented Programming)](http://fsharpforfunandprofit.com/rop/)의 오류 처리 개념이 있다. 그리고 [관측가능한 스트림 (Obsservable Stream)](https://www.youtube.com/watch?v=XE692Clb5LU)(Rx 라이브러리에서 자주 쓰이는 개념)은 비동기 이벤트들을 다루기 위한 모나드 이다. 

그 외에도 엄청나게 많은 종류의 모나드와 개념들이 있다. 하지만 용어들을 일관성하게 정리하기 위해, [fantasy-lan](https://github.com/fantasyland/fantasy-land)나 [typeclassopedia](https://wiki.haskell.org/Typeclassopedia) 같은 설명서들도 있다. 이 들은 자연스러운 함수형 코드를 작성하기 위해 범주론의 다양한 개념들을 정리해 놓았다. 
