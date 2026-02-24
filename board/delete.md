# 게시판 삭제

{% swagger method="delete" path="/v1/admin/boards/{boardId}" baseUrl="" summary="게시판 삭제 (관리자)" %}
{% swagger-description %}
특정 게시판을 삭제합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="boardId" type="Long" required="true" %}
게시판 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
```json
{
  "code": 204,
  "message": "[게시판]이 성공적으로 삭제되었습니다."
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
