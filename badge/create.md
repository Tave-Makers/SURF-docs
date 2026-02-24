# 뱃지 부여

{% swagger method="post" path="/v1/admin/members/badges" baseUrl="" summary="활동 뱃지 부여 (관리자)" %}
{% swagger-description %}
관리자가 회원에게 활동 뱃지를 부여합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="badgeType" type="String" required="true" %}
뱃지 타입
{% endswagger-parameter %}

{% swagger-parameter in="body" name="memberIdList" type="Array" required="true" %}
뱃지를 부여할 회원 ID 목록
{% endswagger-parameter %}

{% swagger-response status="201" description="부여 성공" %}
```json
{
  "code": 201,
  "message": "[활동 뱃지]가 성공적으로 부여되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### BadgeType 값

| 값 | 설명 |
|----|------|
| EXCELLENT_MEMBER_1ST | 우수회원 1위 |
| EXCELLENT_MEMBER_2ND | 우수회원 2위 |
| EXCELLENT_MEMBER_3RD | 우수회원 3위 |
| EXCELLENT_STUDY_1ST | 우수 스터디 |
| ADVANCED_PROJECT_1ST | 심화 프로젝트 1위 |
| ADVANCED_PROJECT_2ND | 심화 프로젝트 2위 |
| COLLABORATIVE_PROJECT_1ST | 연합 프로젝트 1위 |
| COLLABORATIVE_PROJECT_2ND | 연합 프로젝트 2위 |

### Request Body 예시

```json
{
  "badgeType": "EXCELLENT_MEMBER_1ST",
  "memberIdList": [1, 2, 3]
}
```
