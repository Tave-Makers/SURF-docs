# 회원가입

{% swagger method="post" path="/v1/user/members/signup" baseUrl="" summary="자체 회원가입 온보딩" %}
{% swagger-description %}
카카오 로그인 후 추가 정보를 입력하여 회원가입을 요청합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="String" required="true" %}
이름
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tracks" type="Array" required="true" %}
트랙 정보 리스트 (최소 1개)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tracks[].generation" type="Integer" required="true" %}
기수
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tracks[].part" type="String" required="true" %}
파트 (BACKEND, WEB_FRONTEND, APP_FRONTEND, DESIGN, DATA_ANALYSIS, DEEP_LEARNING)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="university" type="String" required="true" %}
대학교
{% endswagger-parameter %}

{% swagger-parameter in="body" name="graduateSchool" type="String" required="false" %}
대학원
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="String" required="true" %}
이메일
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phoneNumber" type="String" required="true" %}
전화번호 (10-11자리)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="profileImageUrl" type="String" required="false" %}
프로필 이미지 URL
{% endswagger-parameter %}

{% swagger-response status="201" description="회원가입 요청 접수" %}
```json
{
  "code": 201,
  "message": "회원가입 요청 접수",
  "data": {
    "memberId": 1,
    "profileImageUrl": "https://example.com/profile.jpg",
    "name": "홍길동",
    "tracks": [
      {
        "generation": 15,
        "part": "BACKEND"
      }
    ],
    "university": "서울과학기술대학교",
    "graduateSchool": null,
    "email": "hong@example.com",
    "phoneNumber": "01012345678"
  }
}
```
{% endswagger-response %}

{% swagger-response status="409" description="이미 존재하는 회원" %}
```json
{
  "code": 409,
  "message": "이미 존재하는 [회원]입니다.",
  "data": null
}
```
{% endswagger-response %}

{% swagger-response status="400" description="유효하지 않은 입력값" %}
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
{% endswagger-response %}
{% endswagger %}

### Part Enum 값

| 값 | 설명 |
|----|------|
| BACKEND | 백엔드 |
| WEB_FRONTEND | 웹 프론트엔드 |
| APP_FRONTEND | 앱 프론트엔드 |
| DESIGN | 디자인 |
| DATA_ANALYSIS | 데이터 분석 |
| DEEP_LEARNING | 딥러닝 |
