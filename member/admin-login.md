# 관리자 페이지 인증

## 1. 관리자 페이지 로그인

### 개요
관리자 페이지에 이메일과 비밀번호로 로그인합니다. 로그인 성공 시 Access Token, 사용자 이름, 역할 정보가 반환됩니다.

### 엔드포인트
`POST /v1/manager/sign-in`

### 인증
- **인증 필요 여부:** 인증 불필요 (Public)
- **권한:** 누구나 접근 가능

### 요청 (Request)

**Headers**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `Content-Type` | String | `application/json` | O |

**Body**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `email` | String | 로그인 이메일 | O |
| `password` | String | 비밀번호 | O |

**요청 예시**

```json
{
  "email": "admin@example.com",
  "password": "password123"
}
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 로그인 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `accessToken` | String | JWT Access Token |
| `username` | String | 로그인한 사용자 이름 |
| `role` | String | 사용자 역할 (`ADMIN`, `PRESIDENT`, `MANAGER`, `MEMBER`) |

**응답 예시**

```json
{
  "code": 200,
  "message": "[관리자 페이지]에 성공적으로 로그인했습니다.",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "username": "홍길동",
    "role": "MANAGER"
  }
}
```

---

## 2. 비밀번호 설정

### 개요
관리자의 비밀번호를 설정(변경)합니다. 로그인된 상태에서 비밀번호를 새로 설정할 수 있습니다.

### 엔드포인트
`PATCH /v1/manager/password`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `Authorization` | String | `Bearer {accessToken}` | O |
| `Content-Type` | String | `application/json` | O |

**Body**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `password` | String | 설정할 비밀번호 | O |

**요청 예시**

```json
{
  "password": "newPassword123"
}
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 비밀번호 설정 완료 |

**응답 예시**

```json
{
  "code": 200,
  "message": "[비밀번호 설정]을 완료했습니다.",
  "data": null
}
```
