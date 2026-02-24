# 스크랩 삭제

{% swagger method="delete" path="/v1/user/scraps/{postId}" baseUrl="" summary="스크랩 삭제" %}
{% swagger-description %}
특정 게시글의 스크랩을 취소합니다. 멱등성이 보장됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="스크랩 삭제 성공" %}
```json
{
  "code": 204,
  "message": "[스크랩]이 성공적으로 삭제되었습니다."
}
```
{% endswagger-response %}
{% endswagger %}
