# 피드백 조회

{% swagger method="get" path="/v1/admin/feedbacks" baseUrl="" summary="피드백 조회 (운영진 전용)" %}
{% swagger-description %}
운영진(ROOT, MANAGER, PRESIDENT)이 피드백을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="size" type="Integer" required="false" %}
페이지 크기 (기본값: 20)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="String" required="false" %}
정렬 (기본값: createdAt,desc)
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[피드백]이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "id": 3,
        "content": "기능을 개선해주세요",
        "createdAt": "2025-10-05T14:50:00"
      },
      {
        "id": 2,
        "content": "버그가 있습니다",
        "createdAt": "2025-10-05T14:49:00"
      }
    ],
    "last": true,
    "numberOfElements": 2
  }
}
```
{% endswagger-response %}

{% swagger-response status="403" description="권한 부족" %}
```json
{
  "code": 403,
  "message": "권한이 부족합니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
