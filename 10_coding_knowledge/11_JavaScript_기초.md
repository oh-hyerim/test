# JavaScript 기초

## JavaScript란?

JavaScript는 웹페이지에 동작과 기능을 추가하는 프로그래밍 언어이다.

버튼을 눌렀을 때 특정 작업을 실행하거나, 입력한 내용을 처리하거나, 서버에서 데이터를 받아 화면에 표시할 때 사용할 수 있다.

## 변수

변수는 데이터를 저장하는 이름이다.

```javascript
const userName = "혜림";
let age = 20;
```

`const`는 값을 바꾸지 않을 때 사용한다.

`let`은 나중에 값을 바꿀 수 있을 때 사용한다.

```javascript
let count = 0;
count = count + 1;
```

## 자료형

JavaScript에서 자주 사용하는 자료형은 다음과 같다.

- 문자열: 글자
- 숫자: 수
- 불리언: 참 또는 거짓
- 배열: 여러 값을 순서대로 저장
- 객체: 여러 정보를 이름과 값으로 저장
- null: 값이 없음을 나타냄
- undefined: 값이 아직 정해지지 않음을 나타냄

```javascript
const name = "혜림";
const age = 20;
const isStudent = true;
const emptyValue = null;
```

## 문자열

문자열은 글자를 의미한다.

```javascript
const greeting = "안녕하세요";
```

문자열을 서로 합칠 수 있다.

```javascript
const firstName = "오";
const lastName = "혜림";
const fullName = firstName + lastName;
```

템플릿 문자열을 사용하면 값을 쉽게 넣을 수 있다.

```javascript
const userName = "혜림";
const message = `안녕하세요, ${userName}님`;
```

## 조건문

조건문은 조건에 따라 다른 코드를 실행한다.

```javascript
const age = 20;

if (age >= 18) {
  console.log("성인입니다.");
} else {
  console.log("미성년자입니다.");
}
```

여러 조건을 확인하려면 `else if`를 사용한다.

```javascript
const score = 85;

if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B");
} else {
  console.log("C");
}
```

## 비교 연산자

조건을 비교할 때 다음 연산자를 사용한다.

- `===`: 같은 값인지 확인
- `!==`: 다른 값인지 확인
- `>`: 큰지 확인
- `<`: 작은지 확인
- `>=`: 크거나 같은지 확인
- `<=`: 작거나 같은지 확인

값과 자료형을 함께 비교할 때는 `===`를 사용하는 것이 안전하다.

## 논리 연산자

여러 조건을 함께 확인할 때 사용한다.

- `&&`: 그리고
- `||`: 또는
- `!`: 아니다

```javascript
const age = 20;
const hasPermission = true;

if (age >= 18 && hasPermission) {
  console.log("작업을 허용합니다.");
}
```

## 함수

함수는 특정 작업을 하나로 묶은 것이다.

```javascript
function sayHello() {
  console.log("안녕하세요.");
}

sayHello();
```

함수에 값을 전달할 수 있다.

```javascript
function greet(name) {
  console.log(`${name}님, 안녕하세요.`);
}

greet("혜림");
```

함수에서 결과를 돌려줄 수도 있다.

```javascript
function add(a, b) {
  return a + b;
}

const result = add(2, 3);
console.log(result);
```

## 배열

배열은 여러 값을 순서대로 저장한다.

```javascript
const fruits = ["사과", "바나나", "포도"];
```

배열의 위치는 0부터 시작한다.

```javascript
console.log(fruits[0]);
```

배열에 값을 추가할 수 있다.

```javascript
fruits.push("오렌지");
```

## 객체

객체는 관련된 정보를 이름과 값의 형태로 저장한다.

```javascript
const user = {
  name: "혜림",
  age: 20,
  isStudent: true
};
```

객체의 값을 사용할 수 있다.

```javascript
console.log(user.name);
console.log(user.age);
```

## 반복문

반복문은 같은 작업을 여러 번 실행할 때 사용한다.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

배열의 모든 값을 확인할 때는 `forEach`를 사용할 수 있다.

```javascript
const fruits = ["사과", "바나나", "포도"];

fruits.forEach((fruit) => {
  console.log(fruit);
});
```

## 오류 처리

오류가 발생할 수 있는 코드는 `try...catch`로 처리할 수 있다.

```javascript
try {
  const data = JSON.parse("잘못된 JSON");
  console.log(data);
} catch (error) {
  console.log("오류가 발생했습니다.");
}
```

오류 내용을 확인할 때는 오류 객체를 기록할 수 있다.

```javascript
try {
  doSomething();
} catch (error) {
  console.error(error);
}
```

## 비동기 작업

서버에 데이터를 요청하는 작업처럼 시간이 걸리는 작업은 비동기로 처리할 수 있다.

`async`와 `await`를 사용하면 비동기 코드를 읽기 쉽게 작성할 수 있다.

```javascript
async function loadData() {
  const response = await fetch("/api/data");
  const data = await response.json();

  console.log(data);
}
```

## JavaScript 코드 작성 원칙

- 변수 이름을 알아보기 쉽게 작성한다.
- 하나의 함수는 하나의 역할만 담당하게 한다.
- 같은 코드를 필요 이상으로 반복하지 않는다.
- 사용자 입력을 그대로 믿지 않는다.
- 오류가 발생할 수 있는 부분을 확인한다.
- 코드를 수정한 뒤 실제로 실행해본다.
- 기존 프로젝트의 코드 스타일을 먼저 확인한다.
