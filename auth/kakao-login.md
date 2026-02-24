# 카카오 로그인

## 카카오 인가 화면 리다이렉트

### 개요
카카오 인가 화면으로 리다이렉트합니다. 클라이언트가 카카오 로그인을 시작할 때 호출하는 엔드포인트입니다.

### 엔드포인트
`GET /login/kakao`

### 인증
- **인증 필요 여부:** 불필요
- **권한:** 없음 (비인증 사용자 접근 가능)

### 요청 (Request)

파라미터 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 302 | Found - 카카오 인가 URL로 리다이렉트 |

응답 본문 없이, `Location` 헤더를 통해 카카오 인가 화면으로 리다이렉트됩니다.

---

---

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

---

## 로그인 흐름

1. 클라이언트가 `GET /login/kakao`를 호출합니다.
2. 서버가 카카오 인가 화면 URL로 302 리다이렉트합니다.
3. 사용자가 카카오 계정으로 로그인 및 동의합니다.
4. 카카오가 `GET /login/oauth2/code/kakao?code=...`로 콜백합니다.
5. 서버가 인가 코드를 카카오 Access Token으로 교환합니다.
6. 서버가 카카오 사용자 정보를 조회하여 회원을 생성 또는 갱신합니다.
7. 서버가 JWT Access Token을 응답 본문에, Refresh Token을 HttpOnly 쿠키에 담아 반환합니다.
8. 클라이언트는 Access Token을 저장하고, Refresh Token은 쿠키에서 자동으로 관리됩니다.
