# 멘션 검색

{% swagger method="get" path="/v1/user/comments/mentions/search" baseUrl="" summary="멘션할 회원 검색 (자동완성)" %}
{% swagger-description %}
이름을 기반으로 멘션 가능한 회원을 검색합니다. 최대 10명이 반환되며, 최신 기수 순으로 정렬됩니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="keyword" type="String" required="true" %}
검색 키워드 (최소 2글자 이상)
{% endswagger-parameter %}

{% swagger-response status="200" description="검색 성공" %}
```json
{
  "code": 200,
  "message": "[멘션 검색]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "memberId": 2,
      "nickname": "홍길동",
      "profileImageUrl": "https://example.com/profile.jpg",
      "firstGeneration": 13
    },
    {
      "memberId": 12,
      "nickname": "홍창준",
      "profileImageUrl": "https://example.com/profile2.jpg",
      "firstGeneration": 15
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="400" description="검색어 2글자 미만" %}
```json
{
  "code": 400,
  "message": "회원 멘션 시 이름은 두 글자 이상 입력해주세요.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}
