# 로그아웃

{% swagger method="post" path="/auth/logout" baseUrl="" summary="로그아웃" %}
{% swagger-description %}
현재 디바이스의 Refresh Token을 무효화하고 쿠키를 삭제합니다.
{% endswagger-description %}

{% swagger-parameter in="cookie" name="refreshToken" type="String" required="false" %}
현재 디바이스의 Refresh Token (없어도 성공 처리)
{% endswagger-parameter %}

{% swagger-response status="204" description="로그아웃 완료" %}
```json
{
  "code": 204,
  "message": "로그아웃 완료",
  "data": null
}
```

**Set-Cookie:** refreshToken 삭제 (MaxAge=0)
{% endswagger-response %}
{% endswagger %}

### 처리 로직

1. 쿠키에서 refreshToken 추출
2. 토큰 유효성 검증
3. Redis에서 해당 토큰 삭제
4. 쿠키 삭제 (MaxAge=0)
5. SecurityContext 정리
