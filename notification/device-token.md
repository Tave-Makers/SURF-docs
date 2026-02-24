# FCM 토큰 등록

{% swagger method="post" path="/v1/user/notifications/device-tokens" baseUrl="" summary="디바이스 FCM 토큰 등록" %}
{% swagger-description %}
디바이스의 FCM 토큰을 서버에 등록합니다. 푸시 알림 수신을 위해 앱 실행 시 또는 토큰 갱신 시 호출해야 합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="String" required="true" %}
FCM 디바이스 토큰
{% endswagger-parameter %}

{% swagger-parameter in="body" name="platform" type="String" required="true" %}
플랫폼 (WEB, ANDROID, IOS)
{% endswagger-parameter %}

{% swagger-response status="200" description="등록 성공" %}
```json
{
  "code": 200,
  "message": "[디바이스 토큰]이 성공적으로 등록되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효성 검증 실패" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Request Body 예시

```json
{
  "token": "cmsVx8tgR0iZK5L9p0Q1x:APA91bFgA...",
  "platform": "IOS"
}
```

### Platform 값

| 값 | 설명 |
|----|------|
| WEB | 웹 브라우저 |
| ANDROID | 안드로이드 앱 |
| IOS | iOS 앱 |
