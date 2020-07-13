# 2. 자바스크립트의 기본

## 2.12. 모듈

### 2.12.1. 모듈이란?
프로그램은 작고 단순한 것에서 크고 복잡한 것으로 진화한다. 그 과정에서 코드의 재활용성을 높이고, 유지보수를 용이하게 하는 기법 중 하나로, 코드를 단위에 따라 쪼갤 수 있다.
이렇게 작은 단위로 구획화 시켜 부품으로 사용하는 기법을 모듈화라고 하며, 그 부품들을 모듈이라고 한다.

모듈화를 통해 다음과 같은 효과를 얻을 수 있다.

- 코드를 재활용할 수 있다.
- 필요한 로직을 빠르게 찾을 수 있다.
- 필요한 로직만 로드하여 메모리 낭비를 줄일 수 있다.

자바스크립트에서는 모듈이라는 개념이 분명하게 존재하지는 않는다.
다만, 호스트 환경에 따라 각각 다른 모듈화 방법을 제공하고 있다.

여기서는 대표적인 호스트 환경인 웹브라우저에서의 모듈화 방법에 대해 알아보자.

> 호스트 환경이란, 자바스크립트가 구동되는 환경을 의미한다.

### 2.12.2. 모듈화

다음은 아주 간단한 페이지이다. 모듈이 없다면, 만약 welcome()이라는 함수가 매우 복잡하고 길고 또, 자주 사용되는 코드였다면, 다른 페이지에서 이 함수가 사용 될 때 또 다시 같은 코드를 새로 불러와야 한다. 유지보수도 어렵고 메모리도 낭비된다.

```jsx
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
</head>

<body>
    <script>
				function welcome() {
				    return 'Hello world'
				};
        alert(welcome());
    </script>
</body>

</html>
```

모듈화 시켜보면

```jsx
function welcome() {
    return 'Hello world'
};
```

```jsx
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <script src="greeting.js"></script>
</head>

<body>
    <script>
        alert(welcome());
    </script>
</body>

</html>
```

이렇게 .js 파일을 따로 빼줌으로써 가독성이 높아진다.
그리고 다음과 같이 다른 페이지에서도 재사용할 수 있다.

```jsx
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <script src="greeting.js"></script>
</head>

<body>
    <script>
        welcome();
    </script>
</body>

</html>
```

.js 파일을 수정하면 이 모듈을 사용하는 모든 페이지에서 한 번에 함수의 동작이 바뀌게 된다. 즉, 유지보수에 유용하다.

### 2.12.3. Node.js의 모듈화

node.js에서도 웹브라우저와 같이 javascript를 모듀로하해서 사용할 수 있다.
require를 통해 외부 JavaScript 파일을 불러오면 외부 .js 파일에 있는 로직을 사용할 수 있게 된다.