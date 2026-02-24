# 내 뱃지 조회

{% swagger method="get" path="/v1/user/members/badges" baseUrl="" summary="마이페이지 활동 뱃지 조회" %}
{% swagger-description %}
마이페이지에서 본인의 활동 뱃지를 조회합니다 (무한스크롤).
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNum" type="Integer" required="false" %}
페이지 번호 (기본값: 0)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageSize" type="Integer" required="false" %}
페이지 크기
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[활동 뱃지]가 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "badgeName": "우수회원 1위",
        "generation": 15,
        "awardedAt": "25.01.15"
      }
    ],
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 1,
    "isLast": true
  }
}
```
{% endswagger-response %}
{% endswagger %}
