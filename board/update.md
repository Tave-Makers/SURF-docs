# 게시판 수정

{% swagger method="patch" path="/v1/admin/boards/{boardId}" baseUrl="" summary="게시판 수정 (관리자)" %}
{% swagger-description %}
특정 게시판을 수정합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="boardId" type="Long" required="true" %}
게시판 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
게시판 이름
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="String" required="true" %}
게시판 타입 (NOTICE)
{% endswagger-parameter %}

{% swagger-response status="200" description="수정 성공" %}
```json
{
  "code": 200,
  "message": "[게시판]이 성공적으로 수정되었습니다.",
  "data": {
    "id": 1,
    "name": "수정된 공지사항",
    "type": "NOTICE"
  }
}
```
{% endswagger-response %}

{% swagger-response status="404" description="게시판 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시판]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
