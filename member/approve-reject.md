# 회원가입 승인/거절

## 회원가입 승인

{% swagger method="patch" path="/v1/admin/members/{memberId}/approve" baseUrl="" summary="회원가입 승인 (관리자)" %}
{% swagger-description %}
관리자가 회원의 회원가입을 승인합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="memberId" type="Long" required="true" %}
회원 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="승인 성공" %}
```json
{
  "code": 200,
  "message": "승인되었습니다.",
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

---

## 회원가입 거절

{% swagger method="patch" path="/v1/admin/members/{memberId}/reject" baseUrl="" summary="회원가입 거절 (관리자)" %}
{% swagger-description %}
관리자가 회원의 회원가입을 거절합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="path" name="memberId" type="Long" required="true" %}
회원 ID
{% endswagger-parameter %}

{% swagger-response status="200" description="거절 성공" %}
```json
{
  "code": 200,
  "message": "거절되었습니다.",
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
