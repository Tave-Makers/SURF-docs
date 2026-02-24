# 게시글 목록 조회

## 내가 작성한 게시글

{% swagger method="get" path="/v1/user/posts/me" baseUrl="" summary="내가 작성한 게시글 목록" %}
{% swagger-description %}
현재 로그인 사용자가 작성한 게시글 목록을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 12)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="String" required="false" %}
정렬 (기본값: postedAt,DESC)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "내가 작성한 [게시글] 목록을 성공적으로 조회했습니다.",
  "data": {
    "content": [
      {
        "postId": 1,
        "title": "게시글 1",
        "content": "내용...",
        "pinned": false,
        "postedAt": "2025-10-05T14:48:00",
        "thumbnailImageUrl": "https://s3.../thumb.jpg",
        "boardId": 1,
        "categoryId": 2,
        "scrappedByMe": false,
        "scrapCount": 5,
        "likedByMe": false,
        "likeCount": 3,
        "commentCount": 2,
        "nickname": "홍길동",
        "isReserved": false,
        "viewCount": 50
      }
    ],
    "hasNext": false
  }
}
```
{% endswagger-response %}
{% endswagger %}

---

## 특정 작성자의 게시글

{% swagger method="get" path="/v1/user/posts/author/{authorId}" baseUrl="" summary="특정 작성자의 게시글 목록" %}
{% swagger-description %}
특정 작성자가 작성한 게시글 목록을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="authorId" type="Long" required="true" %}
작성자 회원 ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 12)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "특정 회원이 작성한 [게시글] 목록을 성공적으로 조회했습니다.",
  "data": {
    "content": [...],
    "hasNext": false
  }
}
```
{% endswagger-response %}
{% endswagger %}

---

## 게시판별 게시글

{% swagger method="get" path="/v1/user/posts/board/{boardId}" baseUrl="" summary="게시판별 게시글 목록" %}
{% swagger-description %}
특정 게시판의 게시글을 조회합니다. category 파라미터로 카테고리 필터링이 가능합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="boardId" type="Long" required="true" %}
게시판 ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="category" type="String" required="false" %}
카테고리명 (미지정 시 전체 조회)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 12)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[게시판]별 [게시글] 목록을 성공적으로 조회했습니다.",
  "data": {
    "content": [...],
    "hasNext": true
  }
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

### 목록 Response 필드 (PostResDTO)

| 필드 | 타입 | 설명 |
|------|------|------|
| postId | Long | 게시글 ID |
| title | String | 제목 |
| content | String | 내용 |
| pinned | Boolean | 상단 고정 여부 |
| postedAt | String | 작성 시간 |
| thumbnailImageUrl | String | 썸네일 이미지 URL |
| boardId | Long | 게시판 ID |
| categoryId | Long | 카테고리 ID |
| scrappedByMe | Boolean | 스크랩 여부 |
| scrapCount | Long | 스크랩 수 |
| likedByMe | Boolean | 좋아요 여부 |
| likeCount | Long | 좋아요 수 |
| commentCount | Long | 댓글 수 |
| nickname | String | 작성자 닉네임 |
| isReserved | Boolean | 예약 게시글 여부 |
| viewCount | Integer | 조회수 |
