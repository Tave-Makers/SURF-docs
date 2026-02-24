# 회원 프로필 수정

## 마이페이지 프로필 수정

### 개요
마이페이지에서 프로필을 수정합니다. 변경하고자 하는 필드만 포함하여 요청합니다. 경력 정보는 생성, 수정, 삭제를 한 번의 요청으로 처리할 수 있습니다.

### 엔드포인트
`PATCH /v1/user/members/profile/update`

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
| `Content-Type` | String | `application/json` | O |

**Body**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `email` | String | 이메일 (이메일 형식) | X |
| `university` | String | 대학교 | X |
| `graduateSchool` | String | 대학원 | X |
| `selfIntroduction` | String | 자기소개 (최대 256자) | X |
| `link` | String | 링크 (최대 1024자) | X |
| `phoneNumber` | String | 전화번호 (8-15자리) | X |
| `phoneNumberPublic` | Boolean | 전화번호 공개 여부 | X |
| `profileImageUrl` | String | 프로필 이미지 URL | X |
| `isProfileImageChanged` | Boolean | 프로필 이미지 변경 여부 | X |
| `careersToCreate` | Array | 생성할 경력 목록 | X |
| `careersToUpdate` | Array | 수정할 경력 목록 | X |
| `careerIdsToDelete` | Array | 삭제할 경력 ID 목록 | X |

**careersToCreate (경력 생성)**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `companyName` | String | 회사명 | O |
| `position` | String | 직무 | O |
| `startDate` | String | 근무 시작일 (YYYY-MM-DD) | O |
| `endDate` | String | 근무 종료일 (YYYY-MM-DD) | X |
| `isWorking` | Boolean | 현재 근무 중 여부 | O |

**careersToUpdate (경력 수정)**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `careerId` | Long | 경력 ID | O |
| `companyName` | String | 회사명 | O |
| `position` | String | 직무 | O |
| `startDate` | String | 근무 시작일 (YYYY-MM-DD) | O |
| `endDate` | String | 근무 종료일 (YYYY-MM-DD) | X |
| `isWorking` | Boolean | 현재 근무 중 여부 | O |

**요청 예시**

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

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 프로필 수정 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `data` | null | 응답 데이터 없음 |

**응답 예시**

```json
{
  "code": 200,
  "message": "마이페이지에서 [프로필 정보]를 수정했습니다.",
  "data": null
}
```

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 | Bad Request | 유효하지 않은 입력값 (이메일 형식, 전화번호 자릿수 등) |

**응답 예시 (400)**

```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
