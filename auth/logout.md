# 로그아웃

## 로그아웃

### 개요
현재 디바이스의 Refresh Token을 무효화하고 쿠키를 삭제합니다. Refresh Token이 없어도 쿠키 삭제는 항상 수행됩니다.

### 엔드포인트
`POST /auth/logout`

### 인증
- **인증 필요 여부:** 불필요
- **권한:** 없음

### 요청 (Request)

**Cookie**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `refreshToken` | String | 현재 디바이스의 Refresh Token | X |

파라미터 및 Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 204 | No Content - 로그아웃 완료 |

**Set-Cookie**

| Key | 설명 |
|-----|------|
| `refreshToken` | 삭제 (MaxAge=0) |

**응답 예시**

```json
{
  "code": 204,
  "message": "로그아웃 완료",
  "data": null
}
```

---

### 처리 로직

1. 쿠키에서 Refresh Token을 추출합니다.
2. 토큰이 유효한 경우 Redis에서 해당 토큰을 삭제합니다.
3. Refresh Token 쿠키를 삭제합니다 (MaxAge=0).
4. SecurityContext를 정리합니다.
