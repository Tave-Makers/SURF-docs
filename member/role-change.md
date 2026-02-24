# 회원 역할 변경

{% swagger method="patch" path="/v1/admin/members/{memberId}/role" baseUrl="" summary="회원 역할 변경 (관리자)" %}
{% swagger-description %}
특정 회원의 역할을 변경합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="memberId" type="Long" required="true" %}
회원 ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="role" type="String" required="true" %}
변경할 역할 (ADMIN, PRESIDENT, MANAGER, MEMBER)
{% endswagger-parameter %}

{% swagger-response status="200" description="역할 변경 성공" %}
```json
{
  "code": 200,
  "message": "회원 역할이 성공적으로 변경되었습니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효하지 않은 역할" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="404" description="회원 없음" %}
```json
{
  "code": 404,
  "message": "존재하지 않는 [회원]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Request Body 예시

```json
{
  "role": "MANAGER"
}
```

### 사용 가능한 Role 값

| 값 | 설명 |
|----|------|
| ADMIN | 관리자 (루트) |
| PRESIDENT | 회장 |
| MANAGER | 매니저 |
| MEMBER | 일반 회원 |
