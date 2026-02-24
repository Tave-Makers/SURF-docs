# 게시글 생성

{% swagger method="post" path="/v1/user/posts" baseUrl="" summary="게시글 생성" %}
{% swagger-description %}
새로운 게시글을 생성합니다. 작성자는 현재 로그인한 사용자로 자동 지정됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="boardId" type="Long" required="true" %}
게시판 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="categoryId" type="Long" required="true" %}
카테고리 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="title" type="String" required="true" %}
게시글 제목
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="String" required="true" %}
게시글 내용
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pinned" type="Boolean" required="false" %}
상단 고정 여부 (기본값: false)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reservedAt" type="String" required="false" %}
예약 시간 (ISO 8601, 미래 시간만 가능)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="imageUrlList" type="Array" required="false" %}
이미지 목록 [{originalUrl, sequence}]
{% endswagger-parameter %}

{% swagger-parameter in="body" name="hasSchedule" type="Boolean" required="false" %}
일정 매핑 여부
{% endswagger-parameter %}

{% swagger-response status="201" description="생성 성공" %}
```json
{
  "code": 201,
  "message": "[게시글]이 성공적으로 생성되었습니다.",
  "data": {
    "postId": 1,
    "title": "만남의 장 공지사항",
    "content": "전반기 만남의 장 안내입니다.",
    "pinned": true,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 2,
    "scrappedByMe": false,
    "scrapCount": 0,
    "likedByMe": false,
    "likeCount": 0,
    "commentCount": 0,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": true,
    "imageUrlList": [
      {
        "imageId": 1,
        "originalUrl": "https://s3.../image.jpg",
        "postId": 1,
        "sequence": 1
      }
    ],
    "isReserved": false,
    "reservedAt": null,
    "viewCount": 0,
    "hasSchedule": false,
    "scheduleId": null
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="필수 필드 누락" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="게시판 또는 카테고리 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시판]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Request Body 예시

```json
{
  "boardId": 1,
  "categoryId": 2,
  "title": "만남의 장 공지사항",
  "content": "전반기 만남의 장 안내입니다.",
  "pinned": true,
  "reservedAt": null,
  "imageUrlList": [
    {
      "originalUrl": "https://s3.../image.jpg",
      "sequence": 1
    }
  ],
  "hasSchedule": false
}
```
