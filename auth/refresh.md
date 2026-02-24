# 토큰 재발급

{% swagger method="post" path="/auth/refresh" baseUrl="" summary="Access Token 재발급" %}
{% swagger-description %}
HttpOnly Refresh Token 쿠키를 이용해 새로운 Access Token을 재발급합니다. Refresh Token Rotation (RTR) 패턴이 적용되어 Refresh Token도 함께 갱신됩니다.
{% endswagger-description %}

{% swagger-parameter in="cookie" name="refreshToken" type="String" required="true" %}
이전 로그인/재발급 시 받은 HttpOnly 쿠키
{% endswagger-parameter %}

{% swagger-response status="200" description="재발급 성공" %}
```json
{
  "code": 200,
  "message": "Access token 재발급 성공",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiJ9..."
  }
}
```

**Set-Cookie:** 새로운 refreshToken (HttpOnly, Secure)
{% endswagger-response %}

{% swagger-response status="401" description="Refresh Token 없음 또는 유효하지 않음" %}
```json
{
  "code": 401,
  "message": "Refresh token이 유효하지 않습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### RTR (Refresh Token Rotation) 동작

- 매 재발급 시 이전 Refresh Token은 Redis에서 즉시 폐기
- 새로운 Refresh Token이 쿠키로 발급
- **재사용 탐지**: 이미 회전된 토큰으로 재발급 시도 시 해당 사용자의 모든 세션 무효화

### JWT Token 구조

**Access Token Payload:**
```json
{
  "sub": "123",
  "role": "ROLE_MEMBER",
  "iat": 1670726000,
  "exp": 1670729600
}
```

**Refresh Token Payload:**
```json
{
  "sub": "123",
  "deviceId": "uuid-string",
  "jti": "uuid-string",
  "iat": 1670726000,
  "exp": 1672540800
}
```
