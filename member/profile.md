# 회원 프로필 조회

## 마이페이지 프로필 정보 조회

### 개요
마이페이지에서 프로필 정보를 조회합니다. `memberId` 파라미터 없이 호출하면 현재 로그인한 사용자 본인의 프로필을 조회합니다.

### 엔드포인트
`GET /v1/user/members/profile`

### 인증
- **인증 필요 여부:** 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `Authorization` | String | `Bearer {accessToken}` | O |

**Query Parameters**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `memberId` | Long | 조회할 회원 ID (없으면 본인 조회) | X |

**요청 예시**

```
GET /v1/user/members/profile
GET /v1/user/members/profile?memberId=2
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 프로필 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `username` | String | 회원 이름 |
| `profileImageUrl` | String | 프로필 이미지 URL |
| `phoneNumberPublic` | Boolean | 전화번호 공개 여부 |
| `phoneNumber` | String | 전화번호 (비공개이고 타인 조회 시 null) |
| `selfIntroduction` | String | 자기소개 |
| `link` | String | 링크 |
| `email` | String | 이메일 |
| `university` | String | 대학교 |
| `graduateSchool` | String | 대학원 |
| `role` | String | 회원 역할 |
| `activityScore` | BigDecimal | 활동 점수 |
| `isActive` | Boolean | 활동 여부 |
| `trackList` | Array | 트랙 정보 리스트 |
| `trackList[].generation` | Integer | 기수 |
| `trackList[].part` | String | 파트 |
| `careerList` | Array | 경력 정보 리스트 |
| `careerList[].careerId` | Long | 경력 ID |
| `careerList[].companyName` | String | 회사명 |
| `careerList[].position` | String | 직무 |
| `careerList[].startDate` | String | 근무 시작일 (YYYY-MM) |
| `careerList[].endDate` | String | 근무 종료일 (YYYY-MM) |
| `careerList[].isWorking` | Boolean | 현재 근무 중 여부 |

**응답 예시**

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
