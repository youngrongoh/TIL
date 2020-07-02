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