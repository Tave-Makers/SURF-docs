# 게시판 생성

{% swagger method="post" path="/v1/admin/boards" baseUrl="" summary="게시판 생성 (관리자)" %}
{% swagger-description %}
새로운 게시판을 생성합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
게시판 이름 (공백 불가)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" required="true" %}
게시판 타입 (NOTICE)
{% endswagger-parameter %}

{% swagger-response status="201" description="생성 성공" %}
```json
{
  "code": 201,
  "message": "[게시판]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 1,
    "name": "공지사항",
    "type": "NOTICE"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효하지 않은 입력값" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
