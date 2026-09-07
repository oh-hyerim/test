# HTTP와 REST API 기초

## HTTP란?

HTTP는 웹 브라우저와 서버가 데이터를 주고받을 때 사용하는 통신 규칙이다.

웹사이트를 열거나 서버에 데이터를 요청할 때 HTTP가 사용된다.

## 요청과 응답

웹 통신은 보통 요청과 응답으로 이루어진다.

1. 클라이언트가 서버에 요청을 보낸다.
2. 서버가 요청을 처리한다.
3. 서버가 클라이언트에 응답을 보낸다.

클라이언트는 웹 브라우저나 앱일 수 있다.

서버는 요청을 받아 데이터를 처리하고 결과를 보내는 프로그램이다.

## URL

URL은 인터넷에서 특정 자원의 위치를 나타내는 주소이다.

예시:

```text
https://example.com/users/1
```

URL의 주요 부분은 다음과 같다.

- `https`: 통신 방법
- `example.com`: 서버 주소
- `/users/1`: 요청하려는 자원의 경로

## HTTP 메서드

HTTP 메서드는 서버에 어떤 작업을 요청하는지 나타낸다.

### GET

데이터를 조회할 때 사용한다.

```text
GET /api/users
```

### POST

새로운 데이터를 만들 때 사용한다.

```text
POST /api/users
```

### PUT

기존 데이터를 전체적으로 수정할 때 사용한다.

```text
PUT /api/users/1
```

### PATCH

기존 데이터의 일부를 수정할 때 사용한다.

```text
PATCH /api/users/1
```

### DELETE

데이터를 삭제할 때 사용한다.

```text
DELETE /api/users/1
```

## 상태 코드

서버는 요청 처리 결과를 상태 코드로 알려준다.

### 성공 상태 코드

- `200 OK`: 요청 성공
- `201 Created`: 새로운 데이터 생성 성공
- `204 No Content`: 성공했지만 응답 내용이 없음

### 클라이언트 오류 상태 코드

- `400 Bad Request`: 요청 형식이 잘못됨
- `401 Unauthorized`: 로그인이 필요함
- `403 Forbidden`: 권한이 없음
- `404 Not Found`: 요청한 대상을 찾을 수 없음

### 서버 오류 상태 코드

- `500 Internal Server Error`: 서버 내부 오류
- `503 Service Unavailable`: 서버를 사용할 수 없음

## REST API란?

REST API는 웹의 자원을 일정한 규칙으로 주고받도록 만든 API 설계 방식이다.

자원은 사용자, 상품, 게시글, 주문 같은 데이터를 뜻한다.

예시:

```text
GET /api/users
GET /api/users/1
POST /api/users
PATCH /api/users/1
DELETE /api/users/1
```

## API 경로 작성

API 경로는 자원의 이름을 사용해 작성하는 것이 좋다.

좋은 예:

```text
/api/users
/api/products
/api/posts
```

좋지 않은 예:

```text
/api/getUsers
/api/createUser
/api/deleteUser
```

어떤 작업을 하는지는 경로 이름보다 HTTP 메서드로 구분하는 것이 좋다.

## 경로 매개변수

경로 매개변수는 특정 데이터를 가리킬 때 사용한다.

예시:

```text
/api/users/10
```

위 주소에서 `10`은 사용자 ID이다.

Express에서 사용하는 예시:

```javascript
app.get("/api/users/:id", (request, response ) => {
  const userId = request.params.id;

  response.json({
    id: userId
  });
});
```

## 쿼리 매개변수

쿼리 매개변수는 검색이나 정렬 같은 추가 조건을 전달할 때 사용한다.

예시:

```text
/api/users?search=hyerim&page=1
```

Express에서 사용하는 예시:

```javascript
app.get("/api/users", (request, response) => {
  const search = request.query.search;
  const page = request.query.page;

  response.json({
    search,
    page
  });
});
```

## 요청 본문

POST, PUT, PATCH 요청에서는 요청 본문에 데이터를 담아 보낼 수 있다.

예시:

```json
{
  "name": "혜림",
  "email": "hyerim@example.com"
}
```

서버에서는 다음과 같이 받을 수 있다.

```javascript
app.use(express.json());

app.post("/api/users", (request, response) => {
  const { name, email } = request.body;

  response.status(201).json({
    name,
    email
  });
});
```

## 응답 형식

API 응답은 일관된 형식으로 작성하는 것이 좋다.

성공 응답 예시:

```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "혜림"
  }
}
```

오류 응답 예시:

```json
{
  "success": false,
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "사용자를 찾을 수 없습니다."
  }
}
```

## API 오류 처리

API 오류가 발생하면 적절한 상태 코드와 설명을 함께 보낸다.

```javascript
app.get("/api/users/:id", async (request, response) => {
  try {
    const user = await findUser(request.params.id);

    if (!user) {
      return response.status(404).json({
        success: false,
        message: "사용자를 찾을 수 없습니다."
      });
    }

    response.json({
      success: true,
      data: user
    });
  } catch (error) {
    console.error(error);

    response.status(500).json({
      success: false,
      message: "서버 오류가 발생했습니다."
    });
  }
});
```

## API 테스트

API는 브라우저, 명령어, API 테스트 도구를 사용해 확인할 수 있다.

GET 요청 예시:

```powershell
Invoke-RestMethod http://localhost:3000/api/users
```

POST 요청 예시:

```powershell
$body = @{
  name = "혜림"
  email = "hyerim@example.com"
} | ConvertTo-Json

Invoke-RestMethod `
  -Method Post `
  -Uri "http://localhost:3000/api/users" `
  -ContentType "application/json" `
  -Body $body
```

API를 테스트할 때는 다음을 확인한다.

- 요청 주소가 맞는가?
- HTTP 메서드가 맞는가?
- 요청 데이터 형식이 맞는가?
- 응답 상태 코드가 예상과 같은가?
- 응답 내용이 올바른가?
- 오류 상황에서 적절한 메시지가 나오는가?

## 인증이 필요한 API

로그인한 사용자만 사용할 수 있는 API에는 인증 확인이 필요하다.

예:

```text
GET /api/profile
POST /api/posts
DELETE /api/posts/1
```

인증이 필요한 API는 사용자가 로그인했는지 확인한 뒤 작업을 실행해야 한다.

## API 보안 원칙

- 사용자 입력을 검증한다.
- 로그인 여부를 확인한다.
- 사용자의 권한을 확인한다.
- 민감한 정보를 응답에 포함하지 않는다.
- 비밀번호를 그대로 반환하지 않는다.
- 오류 응답에 내부 정보나 비밀 정보를 노출하지 않는다.
- 요청 횟수를 제한할 필요가 있는지 확인한다.
- 외부에서 받은 데이터를 무조건 신뢰하지 않는다.

## HTTP와 API 작업 원칙

- API를 만들기 전에 요청과 응답 형식을 정한다.
- 자원에 맞는 URL을 사용한다.
- 작업에 맞는 HTTP 메서드를 사용한다.
- 성공과 오류 상태 코드를 구분한다.
- API 응답 형식을 일관되게 유지한다.
- 입력값을 검증한다.
- 실제로 요청을 보내 기능을 테스트한다.
- 테스트하지 않은 API가 정상이라고 말하지 않는다.
