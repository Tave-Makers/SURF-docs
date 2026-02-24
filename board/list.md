# 게시판 목록 조회

{% swagger method="get" path="/v1/user/boards" baseUrl="" summary="게시판 목록 조회" %}
{% swagger-description %}
모든 게시판을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[게시판]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 1,
      "name": "공지사항",
      "type": "NOTICE"
    },
    {
      "id": 2,
      "name": "자유게시판",
      "type": "NOTICE"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}
