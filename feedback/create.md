# 피드백 생성

{% swagger method="post" path="/v1/user/feedbacks" baseUrl="" summary="익명 피드백 생성" %}
{% swagger-description %}
익명 피드백을 생성합니다. 하루 최대 3회까지 작성할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="content" type="String" required="true" %}
피드백 내용 (최대 500자)
{% endswagger-parameter %}

{% swagger-response status="201" description="생성 성공" %}
```json
{
  "code": 201,
  "message": "[피드백]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 1,
    "content": "더 많은 네트워킹 시간이 있었으면 좋겠습니다.",
    "createdAt": "2025-02-24T14:48:00"
  }
}
```
{% endswagger-response %}

{% swagger-response status="429" description="하루 3회 제한 초과" %}
```json
{
  "code": 429,
  "message": "하루에 3개의 [피드백]만 작성할 수 있습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Request Body 예시

```json
{
  "content": "더 많은 네트워킹 시간이 있었으면 좋겠습니다."
}
```
