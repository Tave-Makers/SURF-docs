# 활동기록 조회

{% swagger method="get" path="/v1/user/members/activity-records" baseUrl="" summary="활동 기록 조회 (무한스크롤)" %}
{% swagger-description %}
본인의 활동 기록을 무한스크롤 방식으로 조회합니다.
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
  "message": "[활동 기록]이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "categoryName": "출석",
        "activityName": "정규 세션 출석",
        "scoreType": "REWARD",
        "appliedScore": 3.0,
        "prefixSum": 103.0,
        "activityDate": "25.02.24"
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

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| categoryName | String | 활동 카테고리명 |
| activityName | String | 활동 유형명 |
| scoreType | String | REWARD(상점) / PENALTY(벌점) |
| appliedScore | BigDecimal | 적용된 점수 |
| prefixSum | BigDecimal | 누적 점수 |
| activityDate | String | 활동 날짜 (YY.MM.DD) |
