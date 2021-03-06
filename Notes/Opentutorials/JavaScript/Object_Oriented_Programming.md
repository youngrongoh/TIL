# 0. Cover

어지러운 상태
정리정돈
서랍에 물건을 넣고 이름을 붙임
우리는 이름만 기억하면 됨
또 짐이 많아지면 서랍을 늘리고, 방을 늘리면서 정리정돈하여 단순화
복잡→단순화→복잡→단순화
코드를 단순화, 그 중 객체를 다룸
객체: 서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것
처음에 이러한 객체가 필요 없을 수 있으나 이런것이 있다는 것을 알아두는 것도 좋다.

# 1.  실습준비

사용할 에디터를 켜고
node.js 혹은 웹브라우저에 내장된 개발자도구의 콘솔을 사용
자바스크립트를 사용하는 어떠한 환경에서도 동일하게 동작하는 순수한 자바스크립트에 있는 기능을 다루는 수업

# 2. 배열과 객체

## 2.1. 객체의 기본

정보시스템의 핵심은 CR, 그리고 더나아가 UD까지
가장 익숙한 데이터 타입인 배열을 다루어보자.

 

```jsx
let memberArray = ['철수', '영희', '민수'];
console.log("memberArray[2]", memberArray[2]);
```

배열의 원소를 가져올 때는 `array[i]`를 사용(0번째부터 시작)
목록만 있으면 되는 경우는 배열
그런데 어떤 정보에 대한 설명이 필요한 경우가 있다. 이때는 객체를 사용.

```jsx
const memberObject = {
    menager: '철수',
    developer: '영희',
    designer: '민수'
}
console.log("memberObject.designer", memberObject.designer);
console.log("memberObject['designer']", memberObject['designer']);
```

배열의 요소를 가져올 때는 `object.element`를 사용
그런데 객체에서도 `['element']`를 사용할 수 있음(따옴표 필수!)
이 두 가지 방법은 맥락에 따라 적절히 사용하면 된다.
이렇게 우리는 읽기, 쓰기를 할 수 있게 되었다.
그럼 수정은 어떻게 할까?

```jsx
const memberObject = {
    menager: '철수',
    developer: '영희',
    designer: '민서'
}
memberObject.designer = '민수';
console.log("memberObject.designer", memberObject.designer);
console.log("memberObject['designer']", memberObject['designer']);
```

민수를 민서로 잘못 입력하였다.
그렇다면 `memberObject.designer = '민수'` 이렇게 수정할 수 있다.
삭제를 하고 싶다면,  delete를 사용하면 된다.

```jsx
const memberObject = {
    menager: '철수',
    developer: '영희',
    designer: '민서'
}
delete memberObject.manager
console.log('after delete memberObject.manager', memberObject.manager);
```

manager 요소가 삭제되어 undefind를 출력하는 것을 볼 수 있다.
객체는 이름이 있는 정보를 정리정돈 하는 도구

## 2.2. 객체와 반복문

배열은 반복문과 만나 거대한 작을 을 할 수 있게 된다.

### 2.2.1. 배열과 반복문

가장 원시적인 반복문, while문을 사용해보자.

```jsx
const memberArray = ['철수', '영희', '민수'];

console.group('array loop');
let i = 0;
while (i < memberArray.length) {
    console.log(memberArray[i]);
    i = i + 1;
}
console.groupEnd('array loop');
```

// tip: `console.group()`과 `console.groupEnd()`를 사용하면 콘솔의 출력 결과를 편하게 볼 수 있다.

### 2.2.2. 객체와 반복문

for문은 배열에서도 사용할 수 있지만 객체에서도 사용할 수 있다. 다만 문법이 다르다.
객체에서는 for ~ in 문이라고 한다.

```jsx
const memberObject = {
    menager: '철수',
    developer: '영희',
    designer: '민서'
}
console.group('object loop');
for (let name in memberObject) {
    console.log(name);
		console.log(memberObject['name']);
}
console.groupEnd('object loop');
```

`for ( let 키값 in 객체){ }` 이러한 문법을 따른다.
반복문을 통해 객체의 속성값을 가져오고 싶다면 어떻게 해야할까.
`object.key`를 통해 객체의 속성값을 호출할 수 있다고 했다.
그러나! 이러한 표현 방식을 사용하면 변수를 사용할 수 없다. 따라서 아래와 같이 undefind가 출력된다.

```jsx
for (let name in memberObject) {
		console.log(memberObject.name); // undefind
		console.log(memberObject[name]);
}
```

이러한 경우에는 대괄호 표현식을 사용하면 된다.(변수에는 따옴표 사용하지 않음!)

# 3. 객체의 사용 사례

## 3.1. 객체는 언제 쓰나요?

자바스크립트에는 수학과 관련된 도구들이 마련되어있다.

```jsx
console.log('Math.PI', Math.PI);
console.log('Math.random()', Math.random());
console.log('Math.floor(3,9)', Math.floor(3.9));
```

이는 자바스크립트를 개발한 이들이 잘 정리정돈하여 넣어둔 것이다.
이 때 객체를 사용한다.
우리는 이렇게 이미 만들어진 객체를 사용하고 있었다.

## 3.2. 객체 만들어 보기

이미 있는 Math객체를 이용해 새로운 객체를 만들어 보자.

```jsx
const MyMath = {
    PI: Math.PI,
    random: function() {
        return Math.random();
    },
    floor: function(value) {
        return Math.floor(value);
    }
}
console.log("MyMath.PI", MyMath.PI);
console.log("MyMath.random", MyMath.random());
console.log("MyMath.floor(3.9)", MyMath.floor(3.9));
```

함수가 객체에 속해있을 때는 메소드라고 한다.
객체는 같은 취지의 서로 연관된 변수와 함수들을 그룹핑해서 거기에 이름을 붙인 것이다.
객체를 반드시 써야만 하는 것은 아니다.  객체 없이도 할 수 있다. 그러나 불편해지고 세련되지 못할 뿐이다. 아래 처럼 말이다.

```jsx
const MyMath_PI = Math.PI;
function MyMath_random() {
    return Math.random();
}
function MyMath_floor(value) {
    return Math.floor(value);
}
```

# 5. this

우리 각자에게는 이름이 있다. 또한 대명사가 있다. 객체에서도 이러한 것이 있다.

```jsx
const kim = {
    name: '김',
    first: 10,
    second: 20,
    sum: function (f, s) {
        return f + s;
    }
}
console.log('kim.sum(kim.first, kim.second)', kim.sum(kim.first, kim.second));
```

함수의 인자로 이미 언급한 것을 다시 중복해서 언급하고 있다.
이를 개선하여보자.

```jsx
const kim = {
    name: '김',
    first: 10,
    second: 20,
    sum: function () {
        return kim.first + kim.second;
    }
}
// console.log('kim.sum(kim.first, kim.second)', kim.sum(kim.first, kim.second));
console.log('kim.sum()', kim.sum());
```

잘 동작한다. 그런데, 객체의 이름이 바뀌면 동작하지 않는다.
그렇게 되면 객체의 이름이 바뀔 때마다 함수도 계속 바꿔줘야하는 번거로움이 발생한다.

이러한 경우에 대명사와 같이 현재의 객체를 가리킬 수 있는 것이 바로, this이다.

```jsx
const k = {
    name: '김',
    first: 10,
    second: 20,
    sum: function () {
        return this.first + this.second;
    }
}
// console.log('kim.sum(kim.first, kim.second)', kim.sum(kim.first, kim.second));
console.log('k.sum()', k.sum());
```

객체의 이름을 바꿔도 잘 동작하게 되었다.

# 6. 객체 공장

## 6.1. constructor의 필요성

```jsx
const kim = {
    name: '김',
    first: 10,
    second: 20,
    sum: function () {
        return this.first + this.second;
    }
}
// console.log('kim.sum(kim.first, kim.second)', kim.sum(kim.first, kim.second));
console.log('kim.sum()', kim.sum());
```

앞서 만든 코드는 하나씩 만들어내는 일종의 가내수공업과 같다.

```jsx
const kim = {
    name: '김',
    first: 10,
    second: 20,
    third: 30,
    sum: function () {
        return this.first + this.second + this.third;
    }
}

const lee = {
    name: '이',
    first: 10,
    second: 10,
    third: 10,
    sum: function () {
        return this.first + this.second + this.third;
    }
}

console.log('kim.sum()', kim.sum());
console.log('lee.sum()', lee.sum());
```

객체의 동작 방식이 바뀌면 그와 연관된 같은 취지의 객체들도 위와 같이 하나 하나 바꿔줘야 한다.
이러한 번거로움을 해결할 수 있는 마치 "객체 공장"과 같은 것이 있다.

## 6.2. constructor의 사례

객체를 찍어내는 사례를 먼저 살펴보자.

```jsx
const d1 = new Date('2019-4-10');
console.log('d1.getFullYear()', d1.getFullYear());
console.log('d1.getMonth()', d1.getMonth());
```

날짜에 관한 정보를 담고 있는 객체가 자바스크립트에 내장되어있다.
이 객체를 사용할 때는 `new`라는 키워드를 통해 새로운 객체를 찍어낼 수 있다.
위에서는 d1이라는 새로운 Date() 객체를 찍어낸 것이다.
그 증거로 우리는 d1에 한 줄의 코드 외에 아무것도 넣지 않았지만 연도와 월에 대한 데이터를 얻어낼 수 있게 된 것이다.

## 6.3. constructor 만들기

우리도 객체를 찍어 내는 공장을 만들어 보자.

`const d1 = new Date('2019-4-10')` 이 부분을 보면 Date는 함수를 호출하는 것처럼 보인다.
Date는 사실 함수이다. 
`console.log('Date', Date)`의 결과를 보면 `Date [Function: Date]`라고 출력되는 것을 볼 수 있다.
즉, 우리는 함수를 만들면 되는 것이다.

```jsx
function Person() {
    this.name = 'kim';
    this.first = 10;
    this.second = 20;
    this.third = 30;
    this.sum = function () {
        return this.first + this.second + this.third;
    }
}

console.log('Person()', Person());
console.log('new Person()', new Person());
```

`console.log('Person()', Person())`의 결과는 undefined가 나온다.
그런데 여기에 `new`라는 키워드를 붙이면 새로운 객체가 만들어진다.

함수를 호출하면 그냥 함수다. 그런데 앞에 new라는 키워드를 붙이면 새로운 객체를 생성하는 생성자(constructor)가 된다.

이를 이용해 kim과 lee 두 객체를 개선해보자.

```jsx
function Person() {
    this.name = 'kim';
    this.first = 10;
    this.second = 20;
    this.third = 30;
    this.sum = function () {
        return this.first + this.second + this.third;
    }
}

const kim = new Person();
const lee = new Person();
console.log('kim.sum()', kim.sum()); // 60
console.log('lee.sum()', lee.sum()); // 60
```

60, 30이 나와야할 값이 동일하게 나왔다.  `const d1 = new Date('2019-4-10')`를 보면 함수에 인자를 넣어줌으로서 입력값을 줄 수 있다. 이것을 도입해보자.

```jsx
function Person(name, first, second, third) {
    this.name = name;
    this.first = first;
    this.second = second;
    this.third = third;
    this.sum = function () {
        return this.first + this.second + this.third;
    }
}

const kim = new Person('kim', 10, 20, 30);
const lee = new Person('lee', 10, 10, 10);
console.log('kim.sum()', kim.sum()); // 60
console.log('lee.sum()', lee.sum()); // 30
```

이렇게 우리는 생성자 함수와 new라는 키워드를 통해 새로운 객체를 찍어낼 수 있게 되었다.

# 7. Prototype

## 7.1. Prototype이 필요한 이유

프로토타입(prototype): 원형, 본래의 모습

JavaScript를 prototype based language라고도 부른다.

```jsx
function Person(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
    this.sum = function () {
        return this.first + this.second;
    }
}
```

Person이라는 생성자가를 통해 새로운 객체가 만들어 질 때마다 sum이라는 함수는 계속해서 새로 만들어진다. 한 두 개의 객체를 생성할 때는 큰 문제가 없겠지만, 1억 개의 객체를 생성한다고 가정하면 이는 엄청난 메모리 낭비를 발생시켜 성능을 저하시키게 된다.

```jsx
const kim = new Person('kim', 10, 20);
```

Person이라는 생성자를 통해 kim이라는 새로운 객체를 만들었다.
만약 kim의 sum함수의 동작을 바꾸고 싶다면 아래와 같이 할 수 있다.

```jsx
kim.sum = function () {
    return 'modified : ' + (this.first + this.second);
}
```

그런데 이런 식으로 바꾸고자 하는 객체가 1천 개라면 이러한 작업을 1천 번 해야한다.
생성자 안에서 함수(메소드)를 정의하면 이러한 불편함이 생기고 생산성이 떨어진다.

## 7.2. Prototype을 이용해서 재사용성을 높이기

그렇다면 동일한 생성자를 사용하는 객체들의 공통된 메소드나 요소를 한 번에 수정해줄 수는 없을까?

```jsx
function Person(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
    
}

Person.prototype.sum = function () {
    return this.first + this.second;
}
```

실행 결과는 이전과 같다.
그러나 sum 함수가 constructor 안에 메소드로서 들어가 있지 않기 때문에, 객체가 만들어질 때마다 새로운 메소드가 만들어지지 않는다.
즉, 한 번만 실행 되므로 성능과 메모리를 절약할 수 있다.
무엇보다, 가장 중요한 효과는 prototype 하나만 수정해도 이를 사용하는 모든 객체에 반영된다는 것이다.

```jsx
const kim = new Person('kim', 10, 20);
kim.sum = function () {
    return 'this : ' + (this.first + this.second);
}
```

위와 같이 일부 객체만 다르게 동작하도록 할 수도 있다.

# 8. Class

## 8.1. Classes

원래 자바스크립트에는 클래스 개념이 없었다.
여러 컴퓨터 언어들은 객체를 만드는 공장과 같은 역할로 class를 채택하고 있다.
앞서 우리는 객체를 찍어내는 공장으로 constructor를 사용했다.
class는 constructor의 대체제로 사용할 수 있다.
JavaScript에는 ECMA 6에서 추가되었다.

우리의 서비스에 새로운 기능을 도입하기에 앞서 [Can I use 닷컴](https://caniuse.com/)에서 브라우저 호환성을 확인해보는 것이 좋다.

또한 [Barbel](https://babeljs.io/)과 같은 컴파일러 혹은 트랜스파일러를 통해 이전 버전의 JavaScript로 변환해줄 수 있다.

## 8.2. Classes의 생산성

```jsx
function Person(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
}

const kim = new Person('kim', 10, 20);
```

Person만 보면 그냥 함수이다.
그런데 new를 붙여 사용하면 이 함수는 객체를 리턴한다.
그리고 객체가 리턴되기 전에 객체의 속성이 기본적으로 세팅된다.
이때, 이 함수는 생성자 construtor가 된다.
constructor는 1)객체를 만들고 2)초기상태를 세팅한다.

그럼 constructor와 동일하게 동작하지만 class를 이용한 코드를 짜보자.

먼저 객체를 만들어보자.

```jsx
class Person {

}

const kim = new Person();  // kim Person {}
```

class를 만들고 kim이라는 객체를 생성했다.

# 9. class construtor

## 9.1. class의 constructor function

class로 객체를 만들 때는 function이라는 키워드 없이 함수명을 바로 쓴다.
객체가 생성될 때, 객체의 초기 상태를 정의하는 약속된 함수를 사용하는데, 바로 constructor이다.

```jsx
class Person {
    constructor() {
        console.log('constructor');
    }
}

const kim = new Person();
console.log('kim', kim);
// constructor
// kim Person {}
```

호출한 적도 없는constructor가 먼저 찍히고 이어서 객체에 대한 `console.log`가 찍혔다.
이는 객체가 생성되는 과정에서 constructor 함수가 실행되었다는 것을 의미한다.

입력값을 주고 초기값을 세팅할 수 있도록 해보자.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
}

const kim = new Person('kim', 10, 20);
console.log('kim', kim); // kim Person { name: 'kim', first: 10, second: 20 }
```

이렇게 객체가 생성될 때 초기값을 세팅하는 constructor를 클래스 내에서 구현하는 방법을 살펴보았다.

# 10. class에서 객체의 method 구현하기

## 10.1. 메소드 구현

Method: 객체에 소속된 함수

이전에 constructor 함수의 prototype 객체를 통해 공통된 함수를 생성하는 우리는 전통적인 방법을 알아보았다.

```jsx
function Person(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
}

Person.prototype.sum = function () {
    return 'modified : ' + (this.first + this.second);
}
```

class 내에서 method를 구현하는 방법을 살펴보자.

가장 간단한 것은 이전의 코드를 그대로 쓰는 것이다.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
}

    Person.prototype.sum = function () {
    return 'prototype : ' + (this.first + this.second);
}
```

 또 한 가지는 class 안에 함수를 넣는 것이다.
이 때, function 키워는 쓰지 않는다!

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return 'prototype : ' + (this.first + this.second);
    }
}
```

어떤 객체에서만 메소드를 다르게 동작하게 하고 싶을 때는 어떻게 할 수 있을까?

```jsx
const kim = new Person('kim', 10, 20);
kim.sum = function () {
    return 'this : ' + (this.first + this.second);
}
```

위와 같이 해당 객체의 메소드를 수정할 수 있다.

# 11. class 상속

## 11.1. 상속

앞서 만든 class에서 평균을 구하는 기능이 필요하다면 어떻게 할 수 있을까?

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return 'prototype : ' + (this.first + this.second);
    }
    avg() {
        return (this.first+this.second)/2;
    }
}
```

이렇게 method를 추가할 수 있을 것이다.
그러나, 만약 우리가 만든 class가 아니라 다른 누군가가 만든 코드거나, library라고 한다면 이 방식으로는 코드를 덮어쓰거나, 수정해선 안되는 상황에 있을 수도 있다.
또한, 평균을 구하는 기능이 아주 조금 쓰이는 경우에는 class 안에 method를 수정하는 것은 부담스러운 일이다.

다른 방법으로는 같은 class를 하나 더 만들 수도 있다.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return 'prototype : ' + (this.first + this.second);
    }
    avg() {
        return (this.first+this.second)/2;
    }
}

class PersonPlus {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return 'prototype : ' + (this.first + this.second);
    }
    avg() {
        return (this.first+this.second)/2;
    }
}
```

그러나 이는 중복된 코드를 발생시키므로 좋은 방법이 아니다.

이를 해결하기 위해 우리는 상속을 사용할 수 있다.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return 'prototype : ' + (this.first + this.second);
    }
}

class PersonPlus extends Person {
    avg() {
        return (this.first+this.second)/2;
    }
}
```

간단하게도 extends를 추가하고 중복되는 코드를 지워주면 된다.

```jsx
const kim = new PersonPlus('kim', 10, 20);
console.log('kim.sum()', kim.sum()); // kim.sum() prototype : 30
console.log('kim.avg()', kim.avg()); // kim.avg() 15
```

PersonPlus는 Person을 상속하므로 PersonPlus에 적지 않은 요소와 메소드를 사용할 수 있다.
PersonPlus를 통해 만든 kim이라는 객체는 Person에 있는 메소드인 sum을 사용할 수 있는 것이다.

# 12. super

## 12.1. super

우리가 기능을 도입할 때마다 복잡성이라는 대가를 치루게 된다.
그리고 복잡성으로 인해 잘 보이지 않는 자잘한 문제들이 생긴다.

상속을 도입함으로써 자식 클래스와 부모 클래스의 관계 문제를 겪을 수 있다. 이를 위해 super라는 키워드를 살펴보자.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return this.first + this.second;
    }
}

class PersonPlus extends Person {
    avg() {
        return (this.first + this.second) / 2;
    }
}

const kim = new PersonPlus('kim', 10, 20);
```

Person은 유지한 채로 kim에서 first, second 외에 third라는 값을 넣고 싶다면 어떻게 해야할까?

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return this.first + this.second;
    }
}

class PersonPlus extends Person {
    constructor(name, first, second, third) {
        this.name = name;
        this.first = first;
        this.second = second;
        this.third = third;
    }
    sum() {
        return this.first + this.second + this.third;
    }
    avg() {
        return (this.first + this.second + this.third) / 3;
    }
}

const kim = new PersonPlus('kim', 10, 20, 30);
```

자식 클래스인 PersonPlus를 이렇게 수정해주면 되지 않을까?
하지만 이렇게 되면 이 코드는 동작하지 않고, 상속을 도입한 이유가 사라진다.
이 때, 우리는 super라는 키워드를 사용할 수 있다.

```jsx
class PersonPlus extends Person {
    constructor(name, first, second, third) {
        super(name, first, second);
        this.third = third;
    }
    sum() {
        return super.sum() + this.third;
    }
    avg() {
        return (this.first + this.second + this.third) / 3;
    }
}
```

class에는 두 가지 용법이 있다.

1. super()는 부모클래스의 생성자를 의미한다. 그래서 자식 클래스의 constructor에서는 super를 쓰고 필요한 요소들을 추가해주면 된다.
2. super.sum과 같이도 사용할 수 있는데, 이 때 super는 부모 클래스를 의미한다.
이렇게 우리는 super를 통해 상속으로 인해 생기는 단점을 보완한 수 있다.

# 13. 객체 간의 상속

## 13.1. object inheritance

객체 지향 프로그래밍은 크게 두 가지 요소로 나누어져 있다.
1) 객체를 만들어 내는 공장인 class
2) class를 통해 만들어진 구체적인 객체가 있다.
이 두 가지 요소가 어떻게 상호 작용하느냐에 따라 다른 형태의 객체지향 언어들이 만들어진다.
JavaScript는 Prototype Based 객체지향 언어이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e85731b-c8a6-436a-b6fa-e160e46d8814/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e85731b-c8a6-436a-b6fa-e160e46d8814/Untitled.png)

주류 객체 지향 언어에서는 subclass가 super class의 자식이 되고 sub class를 통해 객체를 만든다. 그래서 객체는 만들어진 순간 그 기능이 결정된다.

JavaScript에서도 class라는 표현과 extends라는 키워드가 있지만 이는 장식에 불과하다.
JavaScript가 동작하는 내부 매커니즘이 바뀌는 것은 아니며, 다른 언어를 쓰는 개발자들이 쉽게 쓸 수 있도록 해놓은 것 뿐이다.

JavsScript는 다른 객체지향언어들에 비해 자유롭다, 그러나 복잡하고 혼란스러운 면이 있다.

JavaScript에서는 어떤 객체가 다른 어떤 객체로부터 직접 상속 받을 수 있고
링크만 바꿔주면 얼마든지 상속관계를 바꿀 수 있다.
이 링크를 prototype link라고 하고
이 링크가 가리키고 있는 객체를 prototype object라고 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79f19850-4544-4340-83bb-7bee43b9f737/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79f19850-4544-4340-83bb-7bee43b9f737/Untitled.png)

그럼 JavaScript의 객체지향은 어떻게 다른지 살펴보자.

## 13.2. __**proto__**

JavaScript의 클래스 문법이 아닌 전통적인 방법으로 상속을 해보자.

constructor 함수가 아니라 객체를 통해 만들어보자.
JavaScript에서는 클래스가 아닌 인스턴스, 즉 객체를 다른 객체의 자식으로 만들 수 있다.
자식으로 만들길 원하는 객체의 __proto__라는 프로토타입 링크를 사용하면 된다.*

```jsx
var superObj = { superVal: 'super' };
var subObj = { subVal: 'sub' };
subObj.__proto__ = superObj;
console.log('subObj.subVal =>', subObj.subVal);// subObj.subVal => sub
console.log('subObj.superVal =>', subObj.superVal); // subObj.superVal => super
```

*자식 객체에서 상속받은 프로퍼티의 값을 바꾸면, 그 자식 객체의 __proto__에 있는 프로퍼티의 값을 바꾼 것이지, 부모 객체의 프로퍼티의 값을 직접 바꾼 것이 아니다.*

```jsx
subObj.superVal = 'sub';
console.log('subObj.superVal =>', subObj.superVal); // subObj.superVal => super
console.log('superObj.superVal =>', superObj.superVal); // superObj.superVal => super
```

이*렇게 __proto__만 붙여주면 다른 객체의 자식이 된다.
굉장히 유연한 특징이지만 이로 인해 사고의 가능성이 있다.
 __proto__는 JavaScript 표준으로는 인정하고 있지 않다.
그러나 대부분의 브라우저와 자바스크립트가 구동되는 시스템들이 이를 구현하여 제공하고 있긴 하다.

## 13.3. Object.create()

 __proto__의 대체제를 살펴보자.

어떤 객체를 부모로 하는 새로운 객체를 만드는 표준화된 방법은 Object.create()을 이용하는 것이다. __proto__를 사용하는 것보다 Object.create()를 사용해 객체와 객체의 관계를 더 명확하게 지정해주는 것이 좋다.

```jsx
const superObj = { superVal: 'super' };

// var subObj = { subVal: 'sub' };
// subObj.__proto__ = superObj;

const subObj = Object.create(superObj);
subObj.subVal = 'sub';

console.log('subObj.subVal =>', subObj.subVal);// subObj.subVal => sub
console.log('subObj.superVal =>', subObj.superVal); // subObj.superVal => super

subObj.superVal = 'sub';
console.log('subObj.superVal =>', subObj.superVal); // subObj.superVal => super
console.log('superObj.superVal =>', superObj.superVal); // superObj.superVal => super
```

debugger라는 명령을 통해 브라우저에서 Object.create()가__proto__의 값을 변화 시켰을을 확인 해볼 수 있다.

## 13.4. 객체상속의 사용

```jsx
const kim = {
    name: 'kim',
    first: 10, second: 20,
    sum: function () { return this.first + this.second }
}
```

객체를 하나 정의하였다.
그리고 이와 같은 하나의 객체를 더 만들어보려 한다.
그런데 sum이라는 함수를 다시 작성해야 하는 문제가 생긴다.

```jsx
const lee = {
    name: 'lee',
    first: 10, second: 10,
}
```

이 때, 앞서 배운 __**proto**__를 활용할 수 있다.

```jsx
lee.__proto__ = kim;

console.log('lee.sum():', lee.sum()); // lee.sum(): 20
```

lee 객체에서 sum() 함수를 정의하지 않았음에도 __proto__를 통해 kim의 해당 함수를 상속 받아 정상적으로 lee.sum()의 결과가 출력되게 되었다.

또한, kim에는 없으나 lee에서만 새로운 기능을 추가할 수도 있다.

```jsx
const lee = {
    name: 'lee',
    first: 10, second: 10,
    avg: function () {
        return (this.first + this.second) / 2;
    }
}

console.log('lee.avg():', lee.avg()); // lee.avg(): 10
```

lee 객체 안에 함수를 추가해주기만 하면 된다.

이번에는 Object.create()를 사용해서 같은 작업을 해보자.

```jsx
const lee = Object.create(kim);
lee.name = 'lee';
lee.first = 10;
lee.second = 10;
lee.avg = function () {
    return (this.first + this.second) / 2;
}

console.log('lee.sum():', lee.sum()); // lee.sum(): 20
console.log('lee.avg():', lee.avg()); // lee.avg(): 10
```

Object.create()는 표준화된 방법이나, 처음 JavaScript가 나왔을 때부터 있던 것은 아니고, __proto__를 쓰지 않기 위해 도입된 것이므로 아주 구버전의 브라우저에서는 지원하지 않을 수도 있으나 현재로서는 호환성에 큰 문제는 없다고 봐도 무방하다.

# 14. 객체와 함수

## 14.1. 객체와 함수

클래스 기반의 객체 지향언어에서는 클래스가 클래스를 상속하는 것이 아니라 JavaScript에서와 같이 객체가 객체를 상속하고, 런타임 중에 상속을 바꿀 수 있다는 점은 굉장히 기괴한 일이다.

또한 Javascript에서는 함수가 함수 일뿐만 아니라 new를 붙여 객체를 생성하는 생성자가 될 수 있다.

## 14.2. call

```jsx
const kim = { name: 'kim', first: 10, second: 20 };
const lee = { name: 'lee', first: 10, second: 10 };
function sum() {
    return this.first + this.second;
}
```

두 개의 객체를 만들었다. 그런데 앞서 해왔던 것과 다른 점이 있다.
바로, 함수가 객체 안에 메소드로 들어있는 것이 아니라 밖으로 빠져있다.
이런 경우에도 이 함수를 메소드처럼 사용할 수 있다.

아래는 kim이라는 객체 안에 sum이라는 메소드가 있는 경우, 즉 kim.sum()과 같다

```jsx
sum.call(kim);
```

모든 함수는 call이라고 하는 메소드를 가지고 있다.
JavaScript에서는 함수도 객체이기 때문이다.

```jsx
console.log("sum.call(kim) =>", sum.call(kim)); // sum.call(kim) => 30
console.log("sum.call(lee) =>", sum.call(lee)); // sum.call(lee) => 20
```

sum은 kim이라는 객체에 속해있는 메소드가 아니다.
그런데, sum 안에 있는 call이라는 메소드를 통해
마치 sum이 kim 안에 있는 메소드인 것 처럼 실행되었다.

call의 첫번째 인자로 그 함수의 내부적인 this를 무엇으로 할 것인가가 오고
두번째 인자부터는 그 함수의 파라미터들이 오게 된다.

```jsx
function sum2(prefix) {
    return prefix + (this.first + this.second);
}
console.log("sum2.call(kim)", sum2.call(kim, '=> ')); // sum2.call(kim) => 30
console.log("sum2.call(lee)", sum2.call(lee, ': ')); // sum2.call(lee) : 20
```

이렇게 call에 대하여 알아보았다. 참고로, call과 비슷하게 동작하는 apply라는 것도 있다.

## 14.3. bind

call 못지않게 독특한 bind라는 것이 있다.
bind는 묶는다 엮는다는 의미이다.
call은 호출될 때마다 내부의 this를 바꿔주었다면,
bind는 내부적으로 사용할 this를 영구적으로 고정시키는 것이다.

```jsx
const kim = { name: 'kim', first: 10, second: 20 };
const lee = { name: 'lee', first: 10, second: 10 };
function sum(prefix) {
    return prefix + (this.first + this.second);
}

console.log("sum.call(kim)", sum.call(kim, '=> ')); // sum.call(kim) => 30
console.log("sum.call(lee)", sum.call(lee, ': ')); // sum.call(lee) : 20

const kimSum = sum.bind(kim, '-> ');
console.log('kimSum()', kimSum()); // kimSum() -> 30
```

그렇다면, call도 위와 동일한 방법으로 사용할 수는 없을까?

```jsx
const leeSum = sum.call(lee, '->'); // error
```

call은 일시적으로 this를 바꿔준 채로 동작하고 사라지므로 새로운 함수로 할당할 수 없다.

# 15. prototype vs __proto__

## 15.1. prototype vs proto

먼저 함수가 무엇인가에 대해 얘기해보자.

```jsx
function Person(){}
const Person = new Function();
```

위 두 줄의 코드는 서로 같은 것을 의미한다.
JavaScript에서 함수는 객체이다.
그러므로 프로퍼티를 가질 수 있다.

```jsx
function Person(name, first, second) {
	this.name = name;
	this.first = first;
	this.second = second;
}
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12cc8a84-31c4-4f84-aa55-f6867be60215/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12cc8a84-31c4-4f84-aa55-f6867be60215/Untitled.png)

우리가 함수 하나 정의하면 객체가 생긴다.
그런데 또 하나의 객체가 더 생긴다. 그것은 바로 함수의 prototype 객체이다.
이 두 객체는 서로 연관되어 있다.

함수의 객체는 프로토타입 프로퍼티를 가지고 있으며 이 객체는 해당 함수의 프로토타입 객체를 가리킨다.
프로토타입 객체는 constructor 프로퍼티를 가지고 있으며 이는 해당 함수의 객체를 가리킨다.
이렇게 함수의 객체와 프로토타입 객체는 상호참조를 하고 있다.

```jsx
Person.prototype.sum = function(){}
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/663a7a52-5fe0-4e2c-b8b6-8774204b2e94/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/663a7a52-5fe0-4e2c-b8b6-8774204b2e94/Untitled.png)

위와 같이 prototype 프로퍼티에 sum이라는 함수를 정의하면,
프로토타입 객체에 sum 메소드가 생성된다.

위 함수는 new라는 키워드와 함께 객체를 생성할 수 있다.

```jsx
const kim = new Person('kim', 10, 20)
```

이때 함수에 정의되었던 프로퍼티들과 함께 __proto__라고 하는 프로퍼티가 생성된다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1138a219-7b8a-4530-9f00-62b0c2c94044/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1138a219-7b8a-4530-9f00-62b0c2c94044/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61259164-a891-493f-b9d9-d2bc83d04460/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61259164-a891-493f-b9d9-d2bc83d04460/Untitled.png)

이 __proto__라는 프로퍼티는 constructor 함수의 prototype 객체를 가리키게 된다.

그러므로 우리는 constructor 함수의 prototype 프로퍼티와, 동시에 새로 생성된 자식 객체의 __proto__ 프로퍼티 두 가지를 통해 prototype 객체에 접근할 수 있는 것이다.

```jsx
console.log(kim.name);
kim.sum();
```

첫 번째 줄의 코드는 해당 객체에서 해당 프로퍼티가 있는지 찾으며, 있으므로 실행한다.
두 번째 줄의 코드는 해당 객체에서 해당 메소드를 찾는데, 없으므로 __proto__가 가리키는 constructor 객체의 prototype 객체에서 해당 프로퍼티가 있는지 찾고, 있으므로 prototype 객체를 참조하여 실행한다.

# 16. 생성자를 통한 상속

## 16.1. 생성자 함수를 통한 상속

자바스크립트에서 상속을 하는 방법은
객체가 객체를 직접 상속하는 방법과, class 즉 constructor 함수를 이용해 상속하는 방법이 있다.
그 중 class를 사용하는 것이 좀 더 안정적이고 사고 위험이 적다.

## 16.2. 생성자 함수를 통한 상속: 부모 생성자 실행

constructor 함수를 통해 상속을 하는 방법을 알아보자.
앞서 작성한 아래의 class를 통한 상속과 같은 예제를 구현해보겠다.

```jsx
class Person {
    constructor(name, first, second) {
        this.name = name;
        this.first = first;
        this.second = second;
    }
    sum() {
        return this.first + this.second;
    }
}
```

class가 아니라 함수를 만든다.
그리고 class에 sum 메소드를 작성했던 것을 여기서는 constructor 함수의 prototype 객체에 메소드를 추가하는 방식을 사용한다.

```jsx
function Person(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
}
Person.prototype.sum = function () {
    return this.first + this.second;
}
```

constructor 함수를 상속한 함수를 만들어보자.
class로는 아래와 같이 상속했다.

```jsx
class PersonPlus extends Person {
    constructor(name, first, second, third) {
        super(name, first, second);
        this.third = third;
    }
    sum() {
        return super.sum() + this.third;
    }
    avg() {
        return (this.first + this.second + this.third) / 3;
    }
}
```

상속할 함수를 만들고 call()을 실행한다. 그리고 constructor 함수에 없던 메소드는 prototype에 메소드로 추가해주면 된다.

```jsx
function PersonPlus(name, first, second, third) {
    Person.call(this, name, first, second);
    this.third = third;
}
PersonPlus.prototype.avg = function () {
    return (this.first + this.second + this.third) / 3;
}
```

그런데, 아직 끝나지 자식에게 상속되지 않은 것이 있다.
바로 부모의 prototype 객체에 있는 sum이다.

## 16.3. 생성자 함수를 통한 상속: 부모와 연결하기

현재 kim.sum()을 사용할 수 없는 상황이다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9e1c606-b55c-4ba4-9731-a449dac3aa12/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9e1c606-b55c-4ba4-9731-a449dac3aa12/Untitled.png)

어떤 요소가 kim과 kim의 __proto__가 가리키는 PersonPlus의 prototype 객체에 모두 없을 때 PersonPlus의 prototype 객체 안에 있는 __proto__가 PersonPlus의 constructor 함수인 Person의 prototype 객체를 참조하도록 해야 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32167a61-66f1-4c60-9db4-ab3db9abf4b3/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32167a61-66f1-4c60-9db4-ab3db9abf4b3/Untitled.png)

이것은 아주 간단하게도 한 줄의 코드면 된다.

```jsx
PersonPlus.prototype.__proto__ = Person.prototype;
```

그런데 이는 표준이 아니다. 위 코드 대신 Object.create()를 사용해보자.

```jsx
PersonPlus.prototype = Object.create(Person.prototype);
console.log('kim.constructor', kim.constructor); // kim.constructor [Function: Person]
```

그런데, 또 문제가 있다. kim의 constructor가 PersonPlus가 아니라 Person이 되어 버린다.
이를 해결하기 위해서는 아래 코드를 추가해주면 된다.

```jsx
PersonPlus.prototype.constructor = PersonPlus;
console.log('kim.constructor', kim.constructor); // kim.constructor [Function: PersonPlus]
```

## 16.4. 생성자 함수를 통한 상속: constructor 속성은 무엇인가?

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ce4de7b-a5af-4ed3-ad49-85f3e38a7b4e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ce4de7b-a5af-4ed3-ad49-85f3e38a7b4e/Untitled.png)

Person은 prototype을 통해 Person의 prototype 객체를 참조하고,
Person의 prototype 객체는 constructor를 통해 Person을 참조한다.
두 객체는 이렇게 상호참조하고 있다.
그리고, new Person을 통해 만들어진 kim과 lee는 __proto__를 통해 Person의 prototype 객체를 참조한다.
또한, kim.constructor라고 하면 kim에서 찾는데 없으니, __proto___가 가리키는 Person의 prototype에서 찾고, 여기에 있는 constructor가 있으며, 이것은 Person을 가리키고 있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/392f560f-512e-4270-82a7-e65665b46752/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/392f560f-512e-4270-82a7-e65665b46752/Untitled.png)

위와 같이 어떤 객체의 constructor가 무엇인지 몰라도 그것과 같은 constructor를 상속하는 새로운 객체를 만들 수도 있다.

## 16.5. 생성자 함수를 통한 상속: constructor 속성 바로잡기

```jsx
PersonPlus.prototype = Object.create(Person.prototype);

const kim = new PersonPlus('kim', 10, 20, 30);
console.log('kim.constructor', kim.constructor); // kim.constructor [Function: Person]
```

위 방법은 PersonPlus의 prototype을 `Object.create(Person.prototype)`를 통해 새로 만들어진 객체로 대체된다.
그러므로 자연히 `kim.constructor` 곧, PersonPlus의 prototype에 있는 constructor는 Person이 된다.
이것을 해결해보자.

```jsx
PersonPlus.prototype.constructor = PersonPlus;

const kim = new PersonPlus('kim', 10, 20, 30);
console.log('kim.constructor', kim.constructor); // kim.constructor [Function: PersonPlus]
```

다시 PersonPlus.prototype.constructor를 PersonPlus로 바꿔주면 된다.

그런데, 만약 PersonPlus에 메소드를 상속 이전에 추가해버리면 상속이되면서 추가한 메소드는 지워지게 되고 이를 모르고 해당 메소드를 실행하게 되면 오류가 발생하게 된다.

```jsx
PersonPlus.prototype.avg = function () {
    return (this.first + this.second + this.third) / 3;
}

PersonPlus.prototype = Object.create(Person.prototype);
PersonPlus.prototype.constructor = PersonPlus;

const kim = new PersonPlus('kim', 10, 20, 30);
console.log('kim.avg()', kim.avg()); // error
```

__proto__를 쓰면 이러한 문제가 발생하지 않는다.

```jsx
PersonPlus.prototype.avg = function () {
    return (this.first + this.second + this.third) / 3;
}

PersonPlus.prototype.__proto__ = Person.prototype;

const kim = new PersonPlus('kim', 10, 20, 30);
console.log('kim.avg()', kim.avg()); // kim.avg() 20
```

거의 모든 브라우저가 __proto__를 탑재하고 있지만 이는 비표준이므로 Object.create()를 잘 사용하거나, 가장 좋은 방법은 class를 사용하는 것이다. class에서는 이러한 문제가 방생하지 않고, 가독성도 좋다.

그러나 이렇게 constructor를 이용한 방법을 이해해두는 것을 중급으로 가는데 도움을 줄 것이다.