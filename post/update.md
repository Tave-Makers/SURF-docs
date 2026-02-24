# 게시글 수정

{% swagger method="patch" path="/v1/user/posts/{postId}" baseUrl="" summary="게시글 수정" %}
{% swagger-description %}
본인이 작성한 게시글을 수정합니다. 작성자만 수정 가능합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="title" type="String" required="true" %}
수정된 제목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="String" required="true" %}
수정된 내용
{% endswagger-parameter %}

{% swagger-parameter in="body" name="categoryId" type="Long" required="false" %}
카테고리 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pinned" type="Boolean" required="false" %}
상단 고정 여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="isImageChanged" type="Boolean" required="false" %}
이미지 변경 여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="imageUrlList" type="Array" required="false" %}
변경된 이미지 목록
{% endswagger-parameter %}

{% swagger-parameter in="body" name="hasSchedule" type="Boolean" required="false" %}
일정 매핑 여부
{% endswagger-parameter %}

{% swagger-response status="200" description="수정 성공" %}
```json
{
  "code": 200,
  "message": "[게시글]이 성공적으로 수정되었습니다.",
  "data": {
    "postId": 1,
    "title": "수정된 제목",
    "content": "수정된 내용",
    "pinned": false,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 3,
    "scrappedByMe": false,
    "scrapCount": 5,
    "likedByMe": false,
    "likeCount": 3,
    "commentCount": 0,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": true,
    "imageUrlList": [],
    "isReserved": false,
    "reservedAt": null,
    "viewCount": 10,
    "hasSchedule": false,
    "scheduleId": null
  }
}
```
{% endswagger-response %}

{% swagger-response status="401" description="권한 없음" %}
```json
{
  "code": 401,
  "message": "[게시글]을 삭제할 권한이 없습니다.",
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
