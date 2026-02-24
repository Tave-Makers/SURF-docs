# 회원가입

## 자체 회원가입 온보딩

### 개요
카카오 로그인 후 추가 정보를 입력하여 회원가입을 요청합니다. 회원가입 요청 후 관리자의 승인이 필요합니다.

### 엔드포인트
`POST /v1/user/members/signup`

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
| `profileImageUrl` | String | 프로필 이미지 URL | X |
| `name` | String | 이름 | O |
| `tracks` | Array | 트랙 정보 리스트 (최소 1개) | O |
| `tracks[].generation` | Integer | 기수 | O |
| `tracks[].part` | String | 파트 (Part Enum 참조) | O |
| `university` | String | 대학교 | O |
| `graduateSchool` | String | 대학원 | X |
| `email` | String | 이메일 (이메일 형식) | O |
| `phoneNumber` | String | 전화번호 (10-11자리 숫자) | O |

**요청 예시**

```json
{
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
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 201 | Created - 회원가입 요청 접수 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 회원 ID |
| `profileImageUrl` | String | 프로필 이미지 URL |
| `name` | String | 이름 |
| `tracks` | Array | 트랙 정보 리스트 |
| `tracks[].generation` | Integer | 기수 |
| `tracks[].part` | String | 파트 |
| `university` | String | 대학교 |
| `graduateSchool` | String | 대학원 |
| `email` | String | 이메일 |
| `phoneNumber` | String | 전화번호 |

**응답 예시**

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

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 | Bad Request | 유효하지 않은 입력값 |
| 409 | Conflict | 이미 존재하는 회원 |

**응답 예시 (409)**

```json
{
  "code": 409,
  "message": "MEMBER_ALREADY_EXISTS",
  "data": null
}
```

**응답 예시 (400)**

```json
{
  "code": 400,
  "message": "INVALID_ARGUMENT",
  "data": null
}
```

---

## Part Enum

| 값 | 설명 |
|----|------|
| `BACKEND` | 백엔드 |
| `WEB_FRONTEND` | 웹 프론트엔드 |
| `APP_FRONTEND` | 앱 프론트엔드 |
| `DESIGN` | 디자인 |
| `DATA_ANALYSIS` | 데이터 분석 |
| `DEEP_LEARNING` | 딥러닝 |
