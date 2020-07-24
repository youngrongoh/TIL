- 원문: [[번역] 자바스크립트 스코프와 클로저(JavaScript Scope and Closures)](https://medium.com/@khwsc1/%EB%B2%88%EC%97%AD-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80-javascript-scope-and-closures-8d402c976d19)

# 1. 스코프(Scope)

> 자바스크립트에서 스코프란 어떤 변수들에 접근할 수 있는지를 정의한다.

## 1.1. 전역 스코프(Global Scope)

> 변수가 함수 바깥이나 중괄호(`{}`) 바깥에 선언되었다면, 전역 스코프에 정의된다고 한다.

전역 변수는 함수 안팎 등 모든 곳에서 사용할 수 있다.

그러나 변수명 충돌로 오류가 발생할 수 있으므로 전역 스코프에서 변수(let, var)를 선언하는 것은 삼가는 것이 좋다.

## 1.2. 지역 스코프(Local Scope)

선언된 특정 범위에서만 사용할 수 있는 변수를 지역 변수라고 하며, 이 변수들은 지역 스코프에 있다고 할 수 있다.

지역 변수에는 두 가지 종류가 있는데, 함수 스코프(Function scope)와 블록 스코프(Block scope)이다.

### 1.2.1. 함수 스코프(Function Scope)

함수 내에서 선언된 변수는 그 함수 내에서만 유효하다.
그러므로 함수 밖에서 해당 변수에 접근할 수 없다.

### 1.2.2. 블록 스코프(Block Scope)

중괄호(`{}`) 내에서 선언된 변수는 그 블록 안에서만 유효하며, 블록 밖에서는 해당 변수에 접근 할 수 없다.

> 함수를 선언할 때는 중괄호를 사용해야 하므로 블록 스코프는 함수 스코프의 서브셋(subset)입니다.

## 2. 함수 호이스팅과 스코프

함수가 함수 선언식(function declaration, `function name() { }`)으로 선언되면, 현재 스코프의 최상단으로 호이스팅 된다.

다음은 같은 결과를 나타낸다.

```jsx
// This is the same as the one below
sayHello()
function sayHello () {
  console.log('Hello CSS-Tricks Reader!')
}

// This is the same as the code above
function sayHello () {
  console.log('Hello CSS-Tricks Reader!')
}
sayHello()
```

반면, 함수 표현식(function expression, `const name = function () { }`)으로 선언되면, 호이스팅되지 않는다.

함수 사용 방식에 따라 호이스팅이 되기도 하고 그렇지 않기도 하는 특성으로 혼란이 야기될 수 있으므로 항상! 함수를 호출하기 전에 선언해놓는 코딩 습관을 들이는 것이 좋다!

## 3. 네스팅된 스코프(Nested Scope)

다른 함수 내에서 정의된 내부 함수는 외부 함수의 스코프에 있는 변수에 접근할 수 있다.
이를 렉시컬 스코핑(lexical scoping)이라고 한다.

하지만 외부 함수는 내부 함수의 스코프에 있는 변수에 접근할 수 없다.