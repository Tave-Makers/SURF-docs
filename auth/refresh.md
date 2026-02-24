# 토큰 재발급

## Access Token 재발급

### 개요
HttpOnly Refresh Token 쿠키를 이용해 새로운 Access Token을 재발급합니다. Refresh Token Rotation(RTR) 패턴이 적용되어 Refresh Token도 함께 갱신됩니다.

### 엔드포인트
`POST /auth/refresh`

### 인증
- **인증 필요 여부:** 불필요 (Access Token 없이 호출 가능)
- **권한:** 없음 (Cookie에 유효한 Refresh Token이 필요)

### 요청 (Request)

**Cookie**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `refreshToken` | String | 이전 로그인 또는 재발급 시 발급된 HttpOnly 쿠키 | O |

파라미터 및 Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - Access Token 재발급 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `accessToken` | String | 새로 발급된 JWT Access Token |

**Set-Cookie**

| Key | 설명 |
|-----|------|
| `refreshToken` | 새로 발급된 JWT Refresh Token (HttpOnly, Secure) |

**응답 예시**

```json
{
  "code": 200,
  "message": "Access token 재발급 성공",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiJ9..."
  }
}
```

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 | Unauthorized | Refresh Token이 없거나 유효하지 않음 |

**응답 예시 (401)**

```json
{
  "code": 401,
  "message": "Refresh token이 유효하지 않습니다.",
  "data": null
}
```

---

## RTR (Refresh Token Rotation) 동작

RTR은 Refresh Token 탈취에 대한 보안을 강화하기 위한 메커니즘입니다.

1. 클라이언트가 Refresh Token을 사용하여 재발급을 요청합니다.
2. 서버는 기존 Refresh Token을 검증한 후 즉시 폐기(Redis에서 삭제)합니다.
3. 새로운 Refresh Token을 발급하여 HttpOnly 쿠키로 설정합니다.
4. 새로운 Access Token을 응답 본문에 담아 반환합니다.
5. 이미 회전(폐기)된 Refresh Token으로 재발급을 시도하면, 해당 사용자의 모든 세션이 무효화됩니다.
