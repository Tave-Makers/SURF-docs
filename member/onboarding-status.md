# 온보딩 상태 확인

{% swagger method="get" path="/v1/user/members/valid-status" baseUrl="" summary="온보딩 필요 여부 확인" %}
{% swagger-description %}
카카오 로그인 후 추가 정보 입력이 필요한 상태인지 확인합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="상태 확인 성공" %}
```json
{
  "code": 200,
  "message": "[회원]의 추가 회원가입 정보 입력 필요 여부를 확인했습니다.",
  "data": {
    "memberId": 1,
    "needOnboarding": true,
    "memberStatus": "REGISTERING",
    "memberRole": "MEMBER"
  }
}
```
{% endswagger-response %}
{% endswagger %}

### MemberStatus 값

| 값 | 설명 |
|----|------|
| REGISTERING | 가입 중 |
| WAITING | 승인 대기 중 |
| APPROVED | 승인됨 |
| REJECTED | 거절됨 |
| WITHDRAWN | 탈퇴됨 |

### MemberRole 값

| 값 | 설명 |
|----|------|
| ADMIN | 관리자 (루트) |
| PRESIDENT | 회장 |
| MANAGER | 매니저 |
| MEMBER | 일반 회원 |
