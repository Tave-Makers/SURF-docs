# 댓글 삭제

{% swagger method="delete" path="/v1/user/posts/{postId}/comments/{commentId}" baseUrl="" summary="댓글 삭제" %}
{% swagger-description %}
본인이 작성한 댓글을 삭제합니다. Hard 삭제 처리됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-parameter in="path" name="commentId" type="Long" required="true" %}
댓글 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="삭제 성공" %}
```json
{
  "code": 204,
  "message": "[댓글]이 성공적으로 삭제되었습니다."
}
```
{% endswagger-response %}

{% swagger-response status="403" description="본인 댓글이 아님" %}
```json
{
  "code": 403,
  "message": "본인의 [댓글]이 아닙니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="댓글 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [댓글]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
