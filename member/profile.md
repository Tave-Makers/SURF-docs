# 회원 프로필 조회

{% swagger method="get" path="/v1/user/members/profile" baseUrl="" summary="마이페이지 프로필 정보 조회" %}
{% swagger-description %}
마이페이지에서 프로필 정보를 조회합니다. memberId 파라미터 없이 호출하면 본인 프로필을 조회합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="query" name="memberId" type="Long" required="false" %}
조회할 회원 ID (없으면 현재 사용자)
{% endswagger-parameter %}

{% swagger-response status="200" description="프로필 조회 성공" %}
```json
{
  "code": 200,
  "message": "본인 마이페이지에서 [프로필 정보]를 조회합니다.",
  "data": {
    "username": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "phoneNumberPublic": true,
    "phoneNumber": "01012345678",
    "selfIntroduction": "안녕하세요!",
    "link": "https://github.com/example",
    "email": "hong@example.com",
    "university": "서울과학기술대학교",
    "graduateSchool": null,
    "role": "MEMBER",
    "activityScore": 85.5,
    "isActive": true,
    "trackList": [
      {
        "generation": 15,
        "part": "BACKEND"
      }
    ],
    "careerList": [
      {
        "careerId": 1,
        "companyName": "네이버",
        "position": "백엔드 엔지니어",
        "startDate": "2020-01",
        "endDate": "2022-12",
        "isWorking": false
      }
    ]
  }
}
```
{% endswagger-response %}
{% endswagger %}

### Response 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| username | String | 회원 이름 |
| profileImageUrl | String | 프로필 이미지 URL |
| phoneNumberPublic | Boolean | 전화번호 공개 여부 |
| phoneNumber | String | 전화번호 |
| selfIntroduction | String | 자기소개 (최대 256자) |
| link | String | 링크 (최대 1024자) |
| email | String | 이메일 |
| university | String | 대학교 |
| graduateSchool | String | 대학원 |
| role | String | 회원 역할 |
| activityScore | BigDecimal | 활동 점수 |
| isActive | Boolean | 활동/비활동 여부 |
| trackList | Array | 트랙 정보 리스트 |
| careerList | Array | 경력 정보 리스트 |
