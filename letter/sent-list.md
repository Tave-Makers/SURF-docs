# 보낸 쪽지 목록

{% swagger method="get" path="/v1/user/letters/sent" baseUrl="" summary="보낸 쪽지 목록 조회" %}
{% swagger-description %}
자신이 보낸 쪽지 목록을 조회합니다 (최신순).
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 10)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[쪽지] 보낸 목록이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "letterId": 12,
        "title": "문의드립니다.",
        "content": "안녕하세요, 몇 가지 질문이 있습니다.",
        "sns": "@instagram_user",
        "replyEmail": "sender@example.com",
        "senderId": 1,
        "senderName": "홍길동",
        "receiverId": 3,
        "receiverName": "김영희",
        "createdAt": "2025-12-25T14:12:33"
      }
    ],
    "last": true,
    "numberOfElements": 1
  }
}
```
{% endswagger-response %}
{% endswagger %}
