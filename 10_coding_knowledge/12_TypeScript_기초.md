# TypeScript 기초

## TypeScript란?

TypeScript는 JavaScript에 타입 기능을 추가한 프로그래밍 언어이다.

JavaScript에서는 값의 종류가 잘못되어도 실행할 때까지 발견하지 못하는 경우가 있다. TypeScript는 코드를 실행하기 전에 값의 종류가 올바른지 확인하는 데 도움을 준다.

## 타입이란?

타입은 데이터의 종류를 뜻한다.

자주 사용하는 타입은 다음과 같다.

- `string`: 문자열
- `number`: 숫자
- `boolean`: 참 또는 거짓
- `array`: 여러 값을 저장하는 목록
- `object`: 여러 정보를 묶은 객체
- `null`: 값이 없음
- `undefined`: 값이 정해지지 않음

## 변수에 타입 지정하기

변수 이름 뒤에 콜론과 타입 이름을 작성한다.

```typescript
const userName: string = "혜림";
const age: number = 20;
const isStudent: boolean = true;
```

변수에 지정한 타입과 다른 값을 넣으면 오류가 발생할 수 있다.

```typescript
let count: number = 0;
count = 10;
```

## 배열 타입

배열 안에 들어갈 값의 타입을 지정할 수 있다.

```typescript
const names: string[] = ["혜림", "민수"];
const scores: number[] = [90, 80, 70];
```

다음과 같은 방식으로도 작성할 수 있다.

```typescript
const names: Array<string> = ["혜림", "민수"];
```

## 함수의 매개변수 타입

함수에 전달되는 값의 타입을 지정할 수 있다.

```typescript
function greet(name: string) {
  console.log(`${name}님, 안녕하세요.`);
}

greet("혜림");
```

## 함수의 반환 타입

함수가 반환하는 값의 타입도 지정할 수 있다.

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

문자열을 반환하는 함수는 다음과 같이 작성한다.

```typescript
function getMessage(): string {
  return "안녕하세요.";
}
```

## 객체 타입

객체가 가져야 하는 속성과 타입을 정할 수 있다.

```typescript
const user: {
  name: string;
  age: number;
} = {
  name: "혜림",
  age: 20
};
```

## 타입 별칭

반복해서 사용하는 객체 타입은 `type`으로 이름을 만들 수 있다.

```typescript
type User = {
  name: string;
  age: number;
};

const user: User = {
  name: "혜림",
  age: 20
};
```

## 선택적 속성

어떤 속성이 없어도 되는 경우 속성 이름 뒤에 `?`를 작성한다.

```typescript
type User = {
  name: string;
  age?: number;
};

const user: User = {
  name: "혜림"
};
```

## 여러 타입 허용하기

하나의 값에 여러 타입을 허용하려면 `|`를 사용한다.

```typescript
let id: string | number;

id = "user-1";
id = 1;
```

## 타입 좁히기

여러 타입이 가능한 값은 실제 타입을 확인한 뒤 사용해야 한다.

```typescript
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(0));
  }
}
```

## 인터페이스

`interface`는 객체의 구조를 설명할 때 사용할 수 있다.

```typescript
interface Product {
  name: string;
  price: number;
}

const product: Product = {
  name: "노트북",
  price: 1000000
};
```

## any 사용 시 주의

`any`는 거의 모든 값을 허용하는 타입이다.

```typescript
let value: any = "문자열";
value = 123;
value = true;
```

`any`를 많이 사용하면 TypeScript의 장점이 줄어든다. 가능한 한 정확한 타입을 지정하는 것이 좋다.

## null과 undefined

값이 없을 수 있는 경우 해당 가능성을 타입에 표시한다.

```typescript
let selectedName: string | null = null;
```

값이 없는 상태를 확인한 뒤 사용해야 한다.

```typescript
if (selectedName !== null) {
  console.log(selectedName.toUpperCase());
}
```

## 비동기 함수의 타입

비동기 함수는 보통 `Promise`를 반환한다.

```typescript
async function loadMessage(): Promise<string> {
  return "데이터를 불러왔습니다.";
}
```

## TypeScript를 사용하는 이유

TypeScript를 사용하면 다음과 같은 도움을 받을 수 있다.

- 실행하기 전에 일부 오류를 발견할 수 있다.
- 함수에 어떤 값을 넣어야 하는지 알기 쉽다.
- 객체의 구조를 확인하기 쉽다.
- 자동완성 기능이 좋아진다.
- 큰 프로젝트를 관리하기 쉽다.
- 코드를 수정할 때 실수를 줄일 수 있다.

## TypeScript 작업 원칙

- 변수와 함수에 적절한 타입을 지정한다.
- `any`를 필요 이상으로 사용하지 않는다.
- 타입 오류를 무시하지 않는다.
- 기존 프로젝트의 타입 작성 방식을 먼저 확인한다.
- 타입을 억지로 바꾸기보다 실제 데이터 구조를 확인한다.
- 코드를 수정한 뒤 타입 검사를 실행한다.
- 타입 오류를 해결하지 않은 채 완성되었다고 말하지 않는다.
