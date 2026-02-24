# 게시글 삭제

{% swagger method="delete" path="/v1/user/posts/{postId}" baseUrl="" summary="게시글 삭제" %}
{% swagger-description %}
본인이 작성한 게시글을 삭제합니다. 작성자만 삭제 가능합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
```json
{
  "code": 204,
  "message": "[게시글]이 성공적으로 삭제되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="401" description="권한 없음 (작성자가 아님)" %}
```json
{
  "code": 401,
  "message": "[게시글]을 삭제할 권한이 없습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="게시글 없음 또는 이미 삭제됨" %}
```json
{
  "code": 404,
  "message": "이미 삭제된 [게시글]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
