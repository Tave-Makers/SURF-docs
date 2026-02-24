# 쪽지 전송

{% swagger method="post" path="/v1/user/letters" baseUrl="" summary="쪽지 전송" %}
{% swagger-description %}
다른 회원에게 쪽지를 전송합니다. 수신자에게 이메일과 푸시 알림이 발송됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiverId" type="Long" required="true" %}
수신자 회원 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="title" type="String" required="true" %}
쪽지 제목 (최대 100자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="String" required="true" %}
쪽지 본문 (최대 10000자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sns" type="String" required="false" %}
추가 연락 SNS (최대 100자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="replyEmail" type="String" required="true" %}
회신 받을 이메일 (최대 100자)
{% endswagger-parameter %}

{% swagger-response status="200" description="전송 성공" %}
```json
{
  "code": 200,
  "message": "[쪽지]가 성공적으로 전송되었습니다.",
  "data": {
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
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효성 검증 실패" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="수신자 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [회원]입니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="500" description="이메일 발송 실패" %}
```json
{
  "code": 500,
  "message": "메일 발송에 실패했습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
