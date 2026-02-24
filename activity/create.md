# 활동기록 부여

{% swagger method="post" path="/v1/admin/activity-records" baseUrl="" summary="활동 점수(기록) 부여 (관리자)" %}
{% swagger-description %}
관리자가 회원에게 활동 점수(기록)를 부여합니다. 상점 또는 벌점을 부여할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memberIdList" type="Array" required="true" %}
대상 회원 ID 목록
{% endswagger-parameter %}

{% swagger-parameter in="body" name="activityName" type="String" required="true" %}
활동 유형 (ActivityType Enum)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="activityDate" type="String" required="true" %}
활동 날짜 (YYYY-MM-DD)
{% endswagger-parameter %}

{% swagger-response status="201" description="부여 성공" %}
```json
{
  "code": 201,
  "message": "[활동 기록]이 성공적으로 부여되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### ActivityType (상점)

| 값 | 설명 | 점수 |
|----|------|------|
| ATTENDANCE | 출석 | +3 |
| STUDY_ATTENDANCE | 스터디 출석 | +3 |
| ASSIGNMENT_SUBMISSION | 과제 제출 | +5 |
| BLOG_SUBMISSION | 블로그 제출 | +5 |
| MENTORING_PARTICIPATION | 멘토링 참여 | +5 |
| EVENT_PARTICIPATION | 행사 참여 | +5 |
| EXCELLENT_STUDY | 우수 스터디 | +10 |
| ADVANCED_PROJECT | 심화 프로젝트 | +15 |
| COLLABORATIVE_PROJECT | 연합 프로젝트 | +15 |
| EXCELLENT_MEMBER | 우수 회원 | +20 |

### ActivityType (벌점)

| 값 | 설명 | 점수 |
|----|------|------|
| ABSENCE | 결석 | -5 |
| LATE_SUBMISSION | 지각 제출 | -3 |
| UNEXCUSED_ABSENCE | 무단 결석 | -10 |

### Request Body 예시

```json
{
  "memberIdList": [1, 2, 3],
  "activityName": "ATTENDANCE",
  "activityDate": "2025-02-24"
}
```
