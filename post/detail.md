# 게시글 조회

{% swagger method="get" path="/v1/user/posts/{postId}" baseUrl="" summary="게시글 단건 조회" %}
{% swagger-description %}
특정 게시글을 조회합니다. 스크랩/좋아요 여부는 현재 로그인 사용자 기준입니다.
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
  "message": "[게시글]이 성공적으로 조회되었습니다.",
  "data": {
    "postId": 1,
    "title": "만남의 장 공지사항",
    "content": "전반기 만남의 장 안내입니다.",
    "pinned": true,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 2,
    "scrappedByMe": true,
    "scrapCount": 10,
    "likedByMe": true,
    "likeCount": 5,
    "commentCount": 3,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": false,
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
    "viewCount": 150,
    "hasSchedule": false,
    "scheduleId": null
  }
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

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| postId | Long | 게시글 ID |
| title | String | 제목 |
| content | String | 내용 |
| pinned | Boolean | 상단 고정 여부 |
| postedAt | String | 작성 시간 (ISO 8601) |
| boardId | Long | 게시판 ID |
| categoryId | Long | 카테고리 ID |
| scrappedByMe | Boolean | 현재 사용자 스크랩 여부 |
| scrapCount | Long | 스크랩 수 |
| likedByMe | Boolean | 현재 사용자 좋아요 여부 |
| likeCount | Long | 좋아요 수 |
| commentCount | Long | 댓글 수 |
| nickname | String | 작성자 닉네임 |
| profileImageUrl | String | 작성자 프로필 이미지 |
| isMine | Boolean | 본인 게시글 여부 |
| imageUrlList | Array | 이미지 목록 |
| isReserved | Boolean | 예약 게시글 여부 |
| viewCount | Integer | 조회수 |
| hasSchedule | Boolean | 일정 매핑 여부 |
| scheduleId | Long | 일정 ID |
