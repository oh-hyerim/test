# Node.js 백엔드 기초

## Node.js란?

Node.js는 JavaScript를 웹 브라우저 밖에서도 실행할 수 있게 해주는 환경이다.

Node.js를 사용하면 서버 프로그램, API, 자동화 프로그램, 명령줄 도구 등을 만들 수 있다.

## 백엔드란?

백엔드는 사용자가 직접 보는 화면 뒤에서 작동하는 부분이다.

백엔드는 다음과 같은 작업을 처리한다.

- 사용자 로그인
- 데이터 저장과 조회
- 권한 확인
- 파일 처리
- API 제공
- 다른 서비스와의 연결

## 서버란?

서버는 사용자의 요청을 받고 필요한 작업을 처리한 뒤 응답을 보내는 프로그램이다.

기본적인 흐름은 다음과 같다.

1. 사용자가 요청을 보낸다.
2. 서버가 요청을 받는다.
3. 서버가 필요한 작업을 처리한다.
4. 서버가 결과를 응답한다.

## Node.js 프로젝트 시작하기

Node.js 프로젝트를 시작할 때는 먼저 프로젝트 폴더를 만들고 다음 명령어를 실행한다.

```powershell
npm init -y
```

이 명령어를 실행하면 `package.json` 파일이 만들어진다.

## package.json

`package.json`은 Node.js 프로젝트의 기본 설정 파일이다.

다음과 같은 정보를 저장한다.

- 프로젝트 이름
- 프로젝트 버전
- 실행 명령어
- 설치된 패키지
- 프로젝트 설명

예시:

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "나의 Node.js 프로젝트",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```

## 패키지란?

패키지는 다른 사람이 만들어 둔 기능을 프로젝트에서 사용할 수 있도록 묶어둔 코드이다.

패키지를 설치할 때는 다음 명령어를 사용한다.

```powershell
npm install 패키지이름
```

개발할 때만 필요한 패키지는 다음처럼 설치한다.

```powershell
npm install --save-dev 패키지이름
```

## Express란?

Express는 Node.js에서 서버와 API를 쉽게 만들 수 있도록 도와주는 웹 프레임워크이다.

설치 명령어:

```powershell
npm install express
```

## 간단한 서버 만들기

```javascript
const express = require("express");

const app = express();
const port = 3000;

app.get("/", (request, response) => {
  response.send("서버가 정상적으로 작동합니다.");
});

app.listen(port, () => {
  console.log(`서버가 http://localhost:${port}에서 실행 중입니다.` );
});
```

이 서버는 `/` 주소로 요청이 들어오면 문장을 응답한다.

## 서버 실행하기

파일 이름이 `index.js`라면 다음 명령어로 실행할 수 있다.

```powershell
node index.js
```

서버를 종료하려면 터미널에서 다음 키를 누른다.

```text
Ctrl + C
```

## 라우팅

라우팅은 주소와 요청 방법에 따라 어떤 작업을 실행할지 정하는 것이다.

```javascript
app.get("/about", (request, response) => {
  response.send("소개 페이지입니다.");
});
```

자주 사용하는 HTTP 요청 방법은 다음과 같다.

- `GET`: 데이터 조회
- `POST`: 데이터 생성
- `PUT`: 데이터 전체 수정
- `PATCH`: 데이터 일부 수정
- `DELETE`: 데이터 삭제

## JSON 응답

서버에서 JSON 데이터를 보내려면 `response.json()`을 사용한다.

```javascript
app.get("/api/user", (request, response) => {
  response.json({
    name: "혜림",
    age: 20
  });
});
```

## JSON 요청 받기

클라이언트가 보낸 JSON 데이터를 읽으려면 JSON 미들웨어를 사용한다.

```javascript
const express = require("express");

const app = express();

app.use(express.json());

app.post("/api/users", (request, response) => {
  const user = request.body;

  response.json({
    message: "사용자가 등록되었습니다.",
    user
  });
});
```

## 상태 코드

HTTP 상태 코드는 요청 결과를 숫자로 나타낸다.

자주 사용하는 상태 코드는 다음과 같다.

- `200`: 요청 성공
- `201`: 데이터 생성 성공
- `400`: 잘못된 요청
- `401`: 인증 필요
- `403`: 권한 없음
- `404`: 대상을 찾을 수 없음
- `500`: 서버 내부 오류

상태 코드를 지정하는 예시:

```javascript
app.post("/api/users", (request, response) => {
  response.status(201).json({
    message: "생성되었습니다."
  });
});
```

## 요청 데이터 확인

사용자가 보낸 값은 항상 확인해야 한다.

```javascript
app.post("/api/users", (request, response) => {
  const { name, email } = request.body;

  if (!name || !email) {
    return response.status(400).json({
      message: "이름과 이메일은 필수입니다."
    });
  }

  response.status(201).json({
    message: "사용자 정보가 올바릅니다."
  });
});
```

## 오류 처리

서버 오류가 발생했을 때 프로그램이 갑자기 종료되지 않도록 오류를 처리해야 한다.

```javascript
app.get("/api/data", async (request, response) => {
  try {
    const data = await loadData();

    response.json(data);
  } catch (error) {
    console.error(error);

    response.status(500).json({
      message: "데이터를 불러오지 못했습니다."
    });
  }
});
```

## 환경변수 사용

서버 주소나 비밀 정보는 코드에 직접 작성하지 않고 환경변수로 관리할 수 있다.

```javascript
const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`서버가 ${port}번 포트에서 실행 중입니다.`);
});
```

현재 로컬 Ollama만 사용하는 경우에는 외부 API 키가 필요하지 않다.

## CORS

CORS는 다른 주소에서 실행되는 웹페이지가 서버에 요청할 수 있는지 정하는 보안 규칙이다.

프론트엔드와 백엔드가 서로 다른 주소에서 실행될 때 CORS 설정이 필요할 수 있다.

## Node.js 작업 원칙

- 요청 데이터를 항상 확인한다.
- 오류를 사용자에게 이해할 수 있는 응답으로 전달한다.
- 비밀번호와 API 키를 코드에 직접 작성하지 않는다.
- 데이터베이스 작업 전 입력값을 검증한다.
- 운영 서버와 개발 서버를 구분한다.
- 서버를 실행하기 전에 필요한 패키지를 확인한다.
- 포트 충돌이 발생하면 이미 실행 중인 프로그램이 있는지 확인한다.
- 코드를 수정한 뒤 서버를 다시 실행하고 API를 테스트한다.
- 테스트하지 않은 API가 정상이라고 말하지 않는다.
