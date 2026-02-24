# 회원 검색

{% swagger method="get" path="/v1/user/members" baseUrl="" summary="회원 이름/학교 검색 (기수/파트 필터링)" %}
{% swagger-description %}
회원 이름 및 학교로 검색하며, 기수/파트로 필터링할 수 있습니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNum" type="Integer" required="true" %}
페이지 번호 (0부터 시작)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageSize" type="Integer" required="true" %}
페이지 크기
{% endswagger-parameter %}

{% swagger-parameter in="query" name="keyword" type="String" required="false" %}
검색 키워드 (이름 또는 학교)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="generation" type="Integer" required="false" %}
기수 필터 (예: 15)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="part" type="String" required="false" %}
파트 필터 (BACKEND, WEB_FRONTEND 등)
{% endswagger-parameter %}

{% swagger-response status="200" description="검색 성공" %}
```json
{
  "code": 200,
  "message": "[회원 목록]을 검색합니다.",
  "data": {
    "content": [
      {
        "memberId": 1,
        "username": "홍길동",
        "university": "서울과학기술대학교",
        "selfIntroduction": "안녕하세요!",
        "profileImageUrl": "https://example.com/profile.jpg",
        "role": "MEMBER",
        "trackList": [
          {
            "generation": 15,
            "part": "BACKEND"
          }
        ]
      }
    ],
    "totalCount": 1,
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 1,
    "isLast": true
  }
}
```
{% endswagger-response %}
{% endswagger %}
