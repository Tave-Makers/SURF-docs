# 게시글 좋아요

## 좋아요 설정

{% swagger method="post" path="/v1/user/posts/{postId}/like" baseUrl="" summary="게시글 좋아요" %}
{% swagger-description %}
게시글에 좋아요를 설정합니다. 멱등성이 보장됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="좋아요 성공" %}
```json
{
  "code": 200,
  "message": "[게시글] 좋아요가 성공적으로 추가되었습니다.",
  "data": null
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

---

## 좋아요 해제

{% swagger method="delete" path="/v1/user/posts/{postId}/like" baseUrl="" summary="게시글 좋아요 해제" %}
{% swagger-description %}
게시글의 좋아요를 취소합니다. 멱등성이 보장됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="204" description="좋아요 해제 성공" %}
```json
{
  "code": 204,
  "message": "[게시글] 좋아요가 성공적으로 취소되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

---

## 좋아요 목록 조회

{% swagger method="get" path="/v1/user/posts/{postId}/like" baseUrl="" summary="좋아요 누른 사용자 목록" %}
{% swagger-description %}
특정 게시글에 좋아요를 누른 사용자 목록을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[게시글] 좋아요 리스트가 성공적으로 조회되었습니다.",
  "data": {
    "likes": [
      {
        "id": 2,
        "name": "김길동",
        "profileImageUrl": "https://example.com/profile2.jpg"
      }
    ]
  }
}
```
{% endswagger-response %}
{% endswagger %}
