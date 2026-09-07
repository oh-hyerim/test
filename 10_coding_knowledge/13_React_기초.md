# React 기초

## React란?

React는 웹페이지의 화면을 만들기 위한 JavaScript 라이브러리이다.

화면을 여러 개의 작은 컴포넌트로 나누어 만들 수 있다.

## 컴포넌트란?

컴포넌트는 화면을 구성하는 하나의 독립적인 부품이다.

예를 들어 다음과 같은 부분을 각각 컴포넌트로 만들 수 있다.

- 헤더
- 메뉴
- 버튼
- 카드
- 게시글
- 로그인 폼
- 사이드바

컴포넌트를 나누면 코드를 재사용하기 쉽고 관리하기 편하다.

## 컴포넌트 만들기

React 컴포넌트는 보통 대문자로 시작하는 함수로 만든다.

```jsx
function Greeting() {
  return <h1>안녕하세요.</h1>;
}

export default Greeting;
```

컴포넌트는 화면에 표시할 내용을 반환한다.

## JSX란?

JSX는 JavaScript 코드 안에서 HTML과 비슷한 문법을 사용할 수 있게 해주는 문법이다.

```jsx
function Welcome() {
  return <h1>환영합니다.</h1>;
}
```

JSX에서는 HTML과 비슷하지만 몇 가지 규칙이 있다.

- `class` 대신 `className`을 사용한다.
- 여러 요소를 반환할 때 하나의 부모 요소로 감싼다.
- JavaScript 값을 중괄호 `{}` 안에 작성한다.
- 모든 태그를 닫아야 한다.

```jsx
function UserName() {
  const name = "혜림";

  return (
    <div>
      <h1>{name}님</h1>
    </div>
  );
}
```

## Props란?

Props는 부모 컴포넌트가 자식 컴포넌트에 전달하는 값이다.

```jsx
function Greeting({ name }) {
  return <p>{name}님, 안녕하세요.</p>;
}

function App() {
  return <Greeting name="혜림" />;
}
```

위 코드에서 `name`은 `Greeting` 컴포넌트에 전달된 Props이다.

Props는 자식 컴포넌트에서 직접 변경하지 않는다.

## State란?

State는 컴포넌트가 기억하고 관리하는 데이터이다.

State가 변경되면 React는 화면을 다시 표시한다.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 숫자: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        증가
      </button>
    </div>
  );
}
```

위 코드에서:

- `count`: 현재 상태값
- `setCount`: 상태를 변경하는 함수
- `useState(0)`: 초기값이 0이라는 뜻

State를 직접 변경하지 말고 상태 변경 함수를 사용한다.

```jsx
setCount(count + 1);
```

다음처럼 직접 변경하면 안 된다.

```jsx
count = count + 1;
```

## 이벤트 처리

React에서는 사용자의 동작에 함수를 연결할 수 있다.

```jsx
function Button() {
  function handleClick() {
    alert("버튼을 클릭했습니다.");
  }

  return <button onClick={handleClick}>클릭</button>;
}
```

자주 사용하는 이벤트는 다음과 같다.

- `onClick`: 클릭
- `onChange`: 입력값 변경
- `onSubmit`: 폼 제출
- `onMouseEnter`: 마우스가 올라감
- `onKeyDown`: 키보드 키를 누름

## 입력값 관리

입력창의 값을 State로 관리할 수 있다.

```jsx
import { useState } from "react";

function NameForm() {
  const [name, setName] = useState("");

  return (
    <div>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="이름을 입력하세요"
      />
      <p>입력한 이름: {name}</p>
    </div>
  );
}
```

이처럼 React State로 입력값을 관리하는 입력창을 제어 컴포넌트라고 한다.

## 조건부 렌더링

조건에 따라 다른 화면을 표시할 수 있다.

```jsx
function Message({ isLoggedIn }) {
  if (isLoggedIn) {
    return <p>로그인되었습니다.</p>;
  }

  return <p>로그인이 필요합니다.</p>;
}
```

간단한 조건은 삼항 연산자를 사용할 수 있다.

```jsx
function Status({ isOnline }) {
  return <p>{isOnline ? "온라인" : "오프라인"}</p>;
}
```

## 목록 렌더링

배열의 `map`을 사용해 여러 항목을 화면에 표시할 수 있다.

```jsx
function FruitList() {
  const fruits = ["사과", "바나나", "포도"];

  return (
    <ul>
      {fruits.map((fruit) => (
        <li key={fruit}>{fruit}</li>
      ))}
    </ul>
  );
}
```

목록을 표시할 때는 각 항목에 고유한 `key`를 지정해야 한다.

`key`는 React가 목록의 변경사항을 효율적으로 확인하는 데 사용한다.

## useEffect

`useEffect`는 컴포넌트가 화면에 표시되거나 특정 값이 변경될 때 작업을 실행하는 Hook이다.

```jsx
import { useEffect } from "react";

function Example() {
  useEffect(() => {
    console.log("컴포넌트가 표시되었습니다.");
  }, []);

  return <p>예시 화면</p>;
}
```

빈 배열 `[]`을 전달하면 컴포넌트가 처음 표시될 때 한 번 실행된다.

## 서버 데이터 가져오기

React에서는 `fetch`를 사용해 서버에서 데이터를 가져올 수 있다.

```jsx
import { useEffect, useState } from "react";

function UserList() {
  const [users, setUsers] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function loadUsers() {
      try {
        const response = await fetch("/api/users");

        if (!response.ok) {
          throw new Error("사용자 정보를 불러오지 못했습니다.");
        }

        const data = await response.json();
        setUsers(data);
      } catch (error) {
        setError(error.message);
      } finally {
        setIsLoading(false);
      }
    }

    loadUsers();
  }, []);

  if (isLoading) {
    return <p>불러오는 중입니다.</p>;
  }

  if (error) {
    return <p>오류: {error}</p>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

서버 데이터를 사용할 때는 다음 상태를 구분하는 것이 좋다.

- 로딩 중
- 성공
- 오류
- 데이터가 없음

## 컴포넌트 파일 나누기

컴포넌트가 커지면 역할별로 파일을 나눈다.

예시:

```text
src/
├── components/
│   ├── Header.jsx
│   ├── Button.jsx
│   └── UserCard.jsx
├── pages/
│   ├── Home.jsx
│   └── Login.jsx
├── App.jsx
└── main.jsx
```

파일을 나눌 때는 각 컴포넌트가 하나의 분명한 역할을 갖도록 한다.

## React 작업 순서

React 기능을 만들 때는 다음 순서로 진행한다.

1. 필요한 화면과 기능을 정리한다.
2. 화면을 컴포넌트로 나눈다.
3. 필요한 Props와 State를 정한다.
4. 정적인 화면을 먼저 만든다.
5. 사용자 이벤트를 연결한다.
6. 필요한 서버 데이터를 연결한다.
7. 로딩과 오류 상태를 추가한다.
8. 브라우저에서 직접 테스트한다.
9. 기존 기능이 계속 작동하는지 확인한다.

## React 작업 시 주의사항

- 컴포넌트 이름은 대문자로 시작한다.
- State를 직접 변경하지 않는다.
- 목록에는 고유한 `key`를 사용한다.
- Props를 자식 컴포넌트에서 직접 변경하지 않는다.
- 하나의 컴포넌트에 너무 많은 기능을 넣지 않는다.
- 로딩, 오류, 빈 데이터 상태를 처리한다.
- 사용자 입력을 검증한다.
- API 키와 비밀번호를 코드에 직접 넣지 않는다.
- 기존 프로젝트의 React 버전과 작성 방식을 먼저 확인한다.
- 코드를 수정한 뒤 실제 브라우저에서 기능을 테스트한다.
