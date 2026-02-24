# 홈 문구 관리

## 홈 문구 조회

{% swagger method="get" path="/v1/admin/home/content" baseUrl="" summary="홈 문구 조회 (관리자)" %}
{% swagger-description %}
홈 화면에 표시되는 메인 문구를 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[홈 문구]가 성공적으로 조회되었습니다.",
  "data": {
    "mainText": "TAVE와 함께 성장하세요!"
  }
}
```
{% endswagger-response %}
{% endswagger %}

---

## 홈 문구 생성/수정

{% swagger method="put" path="/v1/admin/home/content" baseUrl="" summary="홈 문구 생성/수정 (관리자)" %}
{% swagger-description %}
홈 화면 메인 문구를 생성하거나 수정합니다. 항상 단일 레코드(id=1)로 관리됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mainText" type="String" required="true" %}
메인 문구 (최대 2000자)
{% endswagger-parameter %}

{% swagger-response status="200" description="수정 성공" %}
```json
{
  "code": 200,
  "message": "[홈 문구]가 성공적으로 수정되었습니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
