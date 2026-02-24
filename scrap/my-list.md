# 내 스크랩 목록

{% swagger method="get" path="/v1/user/scraps/me" baseUrl="" summary="내가 스크랩한 게시글 목록" %}
{% swagger-description %}
본인이 스크랩한 게시글 목록을 조회합니다.
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

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[스크랩] 목록이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "postId": 1,
        "title": "만남의 장 공지사항",
        "content": "전반기 만남의 장 안내입니다.",
        "pinned": true,
        "postedAt": "2025-10-05T14:48:00",
        "thumbnailImageUrl": "https://s3.../thumb.jpg",
        "boardId": 1,
        "categoryId": 2,
        "scrappedByMe": true,
        "scrapCount": 10,
        "likedByMe": true,
        "likeCount": 5,
        "commentCount": 0,
        "nickname": "홍길동",
        "isReserved": false,
        "viewCount": 100
      }
    ],
    "last": true,
    "numberOfElements": 1
  }
}
```
{% endswagger-response %}
{% endswagger %}
