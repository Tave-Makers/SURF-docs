# 댓글 좋아요

## 좋아요 토글

{% swagger method="post" path="/v1/user/comments/{commentId}/like" baseUrl="" summary="댓글 좋아요 토글" %}
{% swagger-description %}
댓글 좋아요를 토글합니다. 이미 눌렀으면 취소, 안 눌렀으면 좋아요 처리됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="commentId" type="Long" required="true" %}
댓글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="토글 성공" %}
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 상태가 성공적으로 변경되었습니다.",
  "data": {
    "liked": true
  }
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

---

## 좋아요 개수 조회

{% swagger method="get" path="/v1/user/comments/{commentId}/like/count" baseUrl="" summary="댓글 좋아요 개수 조회" %}
{% swagger-description %}
특정 댓글의 좋아요 개수를 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="commentId" type="Long" required="true" %}
댓글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 개수가 성공적으로 조회되었습니다.",
  "data": 5
}
```
{% endswagger-response %}
{% endswagger %}

---

## 좋아요 여부 조회

{% swagger method="get" path="/v1/user/comments/{commentId}/like/me" baseUrl="" summary="댓글 좋아요 여부 조회" %}
{% swagger-description %}
현재 사용자가 특정 댓글에 좋아요를 눌렀는지 확인합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="commentId" type="Long" required="true" %}
댓글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 상태가 성공적으로 조회되었습니다.",
  "data": true
}
```
{% endswagger-response %}
{% endswagger %}

---

## 좋아요 누른 회원 목록

{% swagger method="get" path="/v1/user/comments/{commentId}/like/members" baseUrl="" summary="댓글 좋아요 누른 회원 목록" %}
{% swagger-description %}
특정 댓글에 좋아요를 누른 회원 목록을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="commentId" type="Long" required="true" %}
댓글 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 누른 회원 목록이 성공적으로 조회되었습니다.",
  "data": [
    {
      "memberId": 5,
      "nickname": "홍길동",
      "profileImageUrl": "https://example.com/profile.jpg"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}
