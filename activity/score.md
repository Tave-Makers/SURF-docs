# 활동점수 조회

{% swagger method="get" path="/v1/user/members/personal-score/pinned5" baseUrl="" summary="개인 활동점수 + 고정 5개 활동기록 조회" %}
{% swagger-description %}
개인 활동점수와 최근 고정된 5개의 활동기록을 함께 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[활동 점수]가 성공적으로 조회되었습니다.",
  "data": {
    "personalScore": 103.0,
    "pinnedRecords": [
      {
        "categoryName": "출석",
        "activityName": "정규 세션 출석",
        "scoreType": "REWARD",
        "appliedScore": 3.0,
        "prefixSum": 103.0,
        "activityDate": "25.02.24"
      }
    ]
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="점수 조회 실패" %}
```json
{
  "code": 400,
  "message": "[개인활동점수]를 조회할 수 없습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### 기본 점수

| 구분 | 초기 점수 |
|------|----------|
| YB (신입) | 100점 |
| 기존 회원 | 50점 |
