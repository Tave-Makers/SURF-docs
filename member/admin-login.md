# 관리자 페이지 로그인

## 관리자 페이지 로그인

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
