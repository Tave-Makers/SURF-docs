# 알림 조회

{% swagger method="get" path="/v1/user/notifications" baseUrl="" summary="알림 조회" %}
{% swagger-description %}
현재 사용자의 알림을 조회합니다. category로 필터링할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="category" type="String" required="false" %}
알림 카테고리 필터 (ACTIVITY, SCHEDULE)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[알람]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 5,
      "type": "POST_LIKE",
      "category": "ACTIVITY",
      "body": "홍길동님이 회원님의 게시글에 좋아요를 남겼습니다.",
      "deepLink": "board/1/post/2",
      "read": false,
      "createdAt": "2025-10-05T14:48:00"
    },
    {
      "id": 3,
      "type": "NOTICE",
      "category": "SCHEDULE",
      "body": "[공지사항] 새로운 공지사항이 업데이트 되었습니다",
      "deepLink": "board/1/post/1",
      "read": true,
      "createdAt": "2025-10-05T14:46:00"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

### NotificationType 값

| 타입 | 카테고리 | 설명 |
|------|---------|------|
| POST_LIKE | ACTIVITY | 게시글 좋아요 |
| POST_COMMENT | ACTIVITY | 게시글 댓글 |
| COMMENT_LIKE | ACTIVITY | 댓글 좋아요 |
| COMMENT_REPLY | ACTIVITY | 댓글 답글 |
| MESSAGE | ACTIVITY | 쪽지 수신 |
| BADGE_UPDATE | ACTIVITY | 뱃지 업데이트 |
| SCORE_UPDATE | ACTIVITY | 점수 업데이트 |
| NOTICE | SCHEDULE | 공지사항 |

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| id | Long | 알림 ID |
| type | String | 알림 유형 |
| category | String | 카테고리 (ACTIVITY / SCHEDULE) |
| body | String | 알림 본문 |
| deepLink | String | 클릭 시 이동할 딥링크 |
| read | Boolean | 읽음 여부 |
| createdAt | String | 생성 시간 |
