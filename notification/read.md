# 알림 읽음 처리

{% swagger method="patch" path="/v1/user/notifications/{notificationId}/read" baseUrl="" summary="알림 읽음 처리" %}
{% swagger-description %}
특정 알림을 읽음 처리합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="notificationId" type="Long" required="true" %}
알림 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="읽음 처리 성공" %}
```json
{
  "code": 200,
  "message": "[알람]이 성공적으로 읽음 처리되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="알림 없음" %}
```json
{
  "code": 404,
  "message": "요청하신 [알람]을 찾을 수 없습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
