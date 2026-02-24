# 댓글 생성

{% swagger method="post" path="/v1/user/posts/{postId}/comments" baseUrl="" summary="댓글 생성 (루트/대댓글)" %}
{% swagger-description %}
루트 댓글 또는 대댓글을 생성합니다. 대댓글은 parentId를 지정하고, 부모 댓글 작성자를 자동 멘션해야 합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="postId" type="Long" required="true" %}
게시글 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="parentId" type="Long" required="false" %}
부모 댓글 ID (대댓글일 때만, 루트 댓글은 null)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="String" required="true" %}
댓글 내용 (최대 1000자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mentionMemberIds" type="Array" required="false" %}
멘션할 회원 ID 목록
{% endswagger-parameter %}

{% swagger-response status="201" description="생성 성공" %}
```json
{
  "code": 201,
  "message": "[댓글]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 15,
    "postId": 3,
    "rootId": 15,
    "parentId": null,
    "depth": 0,
    "content": "좋은 공지 감사합니다!",
    "memberId": 7,
    "nickname": "민수",
    "profileImageUrl": "https://example.com/profile.jpg",
    "likeCount": 0,
    "liked": false,
    "createdAt": "2025-02-24T10:30:00",
    "mentions": [
      {
        "memberId": 5,
        "nickname": "홍길동"
      }
    ]
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효성 검증 실패" %}
```json
{
  "code": 400,
  "message": "[댓글] 내용은 공백일 수 없습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="게시글 또는 부모 댓글 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### 대댓글 멘션 규칙

- 대댓글 작성 시 부모 댓글 작성자를 **반드시** mentionMemberIds에 포함해야 합니다
- 예외: 본인 댓글에 대한 대댓글은 자기 멘션 검증을 스킵합니다
- 자기 자신을 멘션할 수 없습니다

### Request Body 예시

**루트 댓글:**
```json
{
  "parentId": null,
  "content": "좋은 글이네요!",
  "mentionMemberIds": []
}
```

**대댓글:**
```json
{
  "parentId": 15,
  "content": "동의합니다!",
  "mentionMemberIds": [7]
}
```
