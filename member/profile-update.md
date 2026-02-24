# 회원 프로필 수정

{% swagger method="patch" path="/v1/user/members/profile/update" baseUrl="" summary="회원 프로필 수정" %}
{% swagger-description %}
마이페이지에서 프로필을 수정합니다. 변경하고자 하는 필드만 포함하여 요청합니다.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="String" required="true" %}
Bearer {accessToken}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="String" required="false" %}
이메일 (이메일 형식)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="university" type="String" required="false" %}
대학교
{% endswagger-parameter %}

{% swagger-parameter in="body" name="graduateSchool" type="String" required="false" %}
대학원
{% endswagger-parameter %}

{% swagger-parameter in="body" name="selfIntroduction" type="String" required="false" %}
자기소개 (최대 256자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="link" type="String" required="false" %}
링크 (최대 1024자)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phoneNumber" type="String" required="false" %}
전화번호 (8-15자리)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phoneNumberPublic" type="Boolean" required="false" %}
전화번호 공개 여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="profileImageUrl" type="String" required="false" %}
프로필 이미지 URL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="isProfileImageChanged" type="Boolean" required="false" %}
프로필 이미지 변경 여부
{% endswagger-parameter %}

{% swagger-parameter in="body" name="careersToCreate" type="Array" required="false" %}
생성할 경력 목록
{% endswagger-parameter %}

{% swagger-parameter in="body" name="careersToUpdate" type="Array" required="false" %}
수정할 경력 목록
{% endswagger-parameter %}

{% swagger-parameter in="body" name="careerIdsToDelete" type="Array" required="false" %}
삭제할 경력 ID 목록
{% endswagger-parameter %}

{% swagger-response status="200" description="프로필 수정 성공" %}
```json
{
  "code": 200,
  "message": "마이페이지에서 [프로필 정보]를 수정했습니다.",
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

### Request Body 예시

```json
{
  "email": "newemail@example.com",
  "selfIntroduction": "백엔드 개발자입니다.",
  "phoneNumber": "01098765432",
  "phoneNumberPublic": true,
  "profileImageUrl": "https://example.com/new.jpg",
  "isProfileImageChanged": true,
  "careersToCreate": [
    {
      "companyName": "구글",
      "position": "소프트웨어 엔지니어",
      "startDate": "2024-01-01",
      "endDate": null,
      "isWorking": true
    }
  ],
  "careersToUpdate": [
    {
      "careerId": 1,
      "companyName": "네이버",
      "position": "시니어 엔지니어",
      "startDate": "2020-01-01",
      "endDate": "2022-12-31",
      "isWorking": false
    }
  ],
  "careerIdsToDelete": [2]
}
```

### Career 필드 설명

| 필드 | 타입 | 필수 | 설명 |
|------|------|------|------|
| careerId | Long | 수정 시 필수 | 경력 ID |
| companyName | String | O | 회사명 |
| position | String | O | 직무 |
| startDate | String | O | 근무 시작일 (YYYY-MM-DD) |
| endDate | String | X | 근무 종료일 (YYYY-MM-DD) |
| isWorking | Boolean | O | 현재 근무 중 여부 |
