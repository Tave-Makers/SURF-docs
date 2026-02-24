# 카카오 로그인

## 카카오 인가 화면 리다이렉트

{% swagger method="get" path="/login/kakao" baseUrl="" summary="카카오 로그인 요청" %}
{% swagger-description %}
카카오 인가 화면으로 리다이렉트합니다. 클라이언트가 로그인을 시작할 때 호출합니다.
{% endswagger-description %}

{% swagger-response status="302" description="카카오 인가 URL로 리다이렉트" %}
{% endswagger-response %}
{% endswagger %}

---

## 카카오 로그인 콜백

{% swagger method="get" path="/login/oauth2/code/kakao" baseUrl="" summary="카카오 로그인 콜백" %}
{% swagger-description %}
카카오 인가 후 콜백 엔드포인트입니다. 인가 코드를 JWT Access Token으로 교환하고, Refresh Token은 HttpOnly 쿠키로 설정됩니다.
{% endswagger-description %}

{% swagger-parameter in="query" name="code" type="String" required="true" %}
카카오에서 발급한 인가 코드
{% endswagger-parameter %}

{% swagger-response status="200" description="로그인 성공" %}
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
{% endswagger-response %}

{% swagger-response status="400" description="인가 코드 없음" %}
```json
{
  "code": 400,
  "message": "인가 코드가 없습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="401" description="로그인 실패" %}
```json
{
  "code": 401,
  "message": "로그인 실패",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| nickname | String | 카카오 프로필 닉네임 |
| email | String | 카카오 계정 이메일 |
| accessToken | String | JWT Access Token |
| profileImageUrl | String | 카카오 프로필 이미지 URL |

### 로그인 흐름

1. 클라이언트가 `GET /login/kakao` 호출
2. 카카오 인가 화면으로 리다이렉트
3. 사용자가 카카오 로그인 후 인가
4. 카카오가 `GET /login/oauth2/code/kakao?code=...` 로 리다이렉트
5. 서버가 Access Token + Refresh Token(쿠키) 발급
6. 클라이언트는 accessToken을 저장, refreshToken은 쿠키에서 자동 관리
