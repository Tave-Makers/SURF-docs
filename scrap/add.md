# 스크랩 추가

{% swagger method="post" path="/v1/user/scraps/{postId}" baseUrl="" summary="스크랩 추가" %}
{% swagger-description %}
특정 게시글을 스크랩합니다. 이미 스크랩된 경우에도 멱등성이 보장됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="201" description="스크랩 성공" %}
```json
{
  "code": 201,
  "message": "[스크랩]이 성공적으로 생성되었습니다."
}
```
{% endswagger-response %}

{% swagger-response status="404" description="게시글 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
