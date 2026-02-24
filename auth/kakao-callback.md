# 카카오 로그인 콜백

## 카카오 로그인 콜백

### 개요
카카오 인가 후 콜백 엔드포인트입니다. 카카오에서 전달받은 인가 코드(code)를 JWT Access Token으로 교환하고, Refresh Token은 HttpOnly 쿠키로 설정합니다.

### 엔드포인트
`GET /login/oauth2/code/kakao`

### 인증
- **인증 필요 여부:** 불필요
- **권한:** 없음 (카카오 인가 코드로 인증 처리)

### 요청 (Request)

**Query Parameters**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `code` | String | 카카오에서 발급한 인가 코드 | O |

**요청 예시**

```
GET /login/oauth2/code/kakao?code=KAKAO_AUTHORIZATION_CODE
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
| `nickname` | String | 카카오 프로필 닉네임 |
| `email` | String | 카카오 계정 이메일 |
| `accessToken` | String | JWT Access Token |
| `profileImageUrl` | String | 카카오 프로필 이미지 URL |

**Set-Cookie**

| Key | 설명 |
|-----|------|
| `refreshToken` | JWT Refresh Token (HttpOnly, Secure) |

**응답 예시**

```json
{
  "code": 200,
  "message": "로그인 성공",
  "data": {
    "nickname": "홍길동",
    "email": "hong@example.com",
    "accessToken": "eyJhbGciOiJIUzI1NiJ9...",
    "profileImageUrl": "https://k.kakaocdn.net/.../img.jpg"
  }
}
```

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 | Bad Request | 인가 코드가 없거나 비어 있음 |
| 401 | Unauthorized | 카카오 로그인 처리 중 실패 |

**응답 예시 (400)**

```json
{
  "code": 400,
  "message": "인가 코드가 없습니다.",
  "data": null
}
```

**응답 예시 (401)**

```json
{
  "code": 401,
  "message": "로그인 실패",
  "data": null
}
```
