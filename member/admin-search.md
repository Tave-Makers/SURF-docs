# 관리자 회원 조회

## 이름 기반 회원 조회

{% swagger method="get" path="/v1/admin/members/search" baseUrl="" summary="이름 기반 회원 조회 (관리자)" %}
{% swagger-description %}
이름으로 회원을 검색합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="name" type="String" required="true" %}
검색할 회원 이름
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "'홍길동'(으)로 활동 중인 [회원]을 조회했습니다.",
  "data": [
    {
      "memberId": 1,
      "name": "홍길동",
      "generation": 15,
      "track": "백엔드"
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

---

## 트랙+기수별 회원 전체 조회

{% swagger method="get" path="/v1/admin/members/search/grouped-by-track" baseUrl="" summary="트랙+기수별 회원 전체 출력 (관리자)" %}
{% swagger-description %}
활동 중인 회원 전체를 트랙+기수별로 그룹화하여 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-response status="200" description="조회 성공" %}
```json
{
  "code": 200,
  "message": "[트랙]별로 현재 활동 중인 [회원]을 조회했습니다.",
  "data": {
    "15기-백엔드": [
      {
        "memberId": 1,
        "name": "홍길동"
      },
      {
        "memberId": 2,
        "name": "김영희"
      }
    ],
    "15기-웹 프론트엔드": [
      {
        "memberId": 3,
        "name": "이순신"
      }
    ]
  }
}
```
{% endswagger-response %}
{% endswagger %}
