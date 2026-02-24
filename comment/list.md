# 댓글 목록 조회

{% swagger method="get" path="/v1/user/posts/{postId}/comments" baseUrl="" summary="댓글 목록 조회 (페이징)" %}
{% swagger-description %}
특정 게시글의 루트 댓글과 대댓글을 모두 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 10)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="String" required="false" %}
정렬 기준 (기본값: createdAt,desc)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[댓글]이 성공적으로 조회되었습니다.",
  "data": {
    "comments": [
      {
        "id": 15,
        "postId": 3,
        "rootId": 15,
        "parentId": null,
        "depth": 0,
        "content": "좋은 공지 감사합니다!",
        "memberId": 7,
        "nickname": "민수",
        "profileImageUrl": "https://example.com/profile.jpg",
        "likeCount": 2,
        "liked": false,
        "createdAt": "2025-02-24T10:30:00",
        "mentions": [
          {
            "memberId": 5,
            "nickname": "홍길동"
          }
        ]
      },
      {
        "id": 16,
        "postId": 3,
        "rootId": 15,
        "parentId": 15,
        "depth": 1,
        "content": "동의합니다!",
        "memberId": 5,
        "nickname": "홍길동",
        "profileImageUrl": "https://example.com/profile2.jpg",
        "likeCount": 1,
        "liked": true,
        "createdAt": "2025-02-24T11:00:00",
        "mentions": [
          {
            "memberId": 7,
            "nickname": "민수"
          }
        ]
      }
    ],
    "totalCount": 37,
    "hasNext": true
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
| id | Long | 댓글 ID |
| postId | Long | 게시글 ID |
| rootId | Long | 루트 댓글 ID |
| parentId | Long | 부모 댓글 ID (루트면 null) |
| depth | Integer | 댓글 깊이 (0=루트) |
| content | String | 댓글 내용 |
| memberId | Long | 작성자 회원 ID |
| nickname | String | 작성자 닉네임 |
| profileImageUrl | String | 작성자 프로필 이미지 |
| likeCount | Long | 좋아요 수 |
| liked | Boolean | 현재 사용자 좋아요 여부 |
| createdAt | String | 작성일시 |
| mentions | Array | 멘션된 회원 목록 |
