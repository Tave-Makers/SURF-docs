# 관리자용 회원 관리

## 1. 가입신청 목록 조회

### 개요
관리자 페이지에서 가입신청 목록을 조회합니다. 키워드 검색과 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/manager/registration-list`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

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
| `keyword` | String | 검색 키워드 | X |
| `pageSize` | Integer | 페이지 크기 | O |
| `pageNum` | Integer | 페이지 번호 (0부터 시작) | O |

**요청 예시**

```
GET /v1/manager/registration-list?pageSize=10&pageNum=0
GET /v1/manager/registration-list?keyword=홍길동&pageSize=10&pageNum=0
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `content` | Array | 가입신청 회원 목록 |
| `content[].memberId` | Long | 회원 ID |
| `content[].username` | String | 회원 이름 |
| `content[].university` | String | 대학교 |
| `content[].profileImageUrl` | String | 프로필 이미지 URL |
| `content[].trackList` | Array | 트랙 정보 리스트 |
| `content[].trackList[].generation` | Integer | 기수 |
| `content[].trackList[].part` | String | 파트 |
| `content[].role` | String | 회원 역할 |
| `content[].memberStatus` | String | 가입 상태 (`REGISTERING`, `WAITING`, `APPROVED`, `REJECTED`, `WITHDRAWN`) |
| `content[].createdAt` | String | 가입 신청 일시 (형식: `yy.MM.dd HH:mm`) |
| `pageNumber` | Integer | 현재 페이지 번호 |
| `pageSize` | Integer | 페이지 크기 |
| `numberOfElements` | Integer | 현재 페이지 요소 수 |
| `isLast` | Boolean | 마지막 페이지 여부 |

**응답 예시**

```json
{
  "code": 200,
  "message": "[가입신청 목록]을 조회합니다.",
  "data": {
    "content": [
      {
        "memberId": 1,
        "username": "홍길동",
        "university": "서울과학기술대학교",
        "profileImageUrl": "https://example.com/profile.jpg",
        "trackList": [
          {
            "generation": 15,
            "part": "BACKEND"
          }
        ],
        "role": "MEMBER",
        "memberStatus": "WAITING",
        "createdAt": "25.01.15 14:30"
      }
    ],
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 1,
    "isLast": true
  }
}
```

---

## 2. 유저 상세 조회

### 개요
관리자 페이지에서 특정 유저의 상세 정보를 조회합니다. 프로필, 트랙, 커리어, 활동 점수 등 전체 정보를 포함합니다.

### 엔드포인트
`GET /v1/manager/member/{memberId}`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `Authorization` | String | `Bearer {accessToken}` | O |

**Path Parameters**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 조회할 회원의 ID |

**요청 예시**

```
GET /v1/manager/member/1
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `username` | String | 회원 이름 |
| `profileImageUrl` | String | 프로필 이미지 URL |
| `phoneNumberPublic` | Boolean | 전화번호 공개 여부 |
| `phoneNumber` | String | 전화번호 |
| `selfIntroduction` | String | 자기소개 |
| `link` | String | 개인 링크 |
| `email` | String | 이메일 |
| `university` | String | 대학교 |
| `graduateSchool` | String | 대학원 |
| `role` | String | 역할 (`ADMIN`, `PRESIDENT`, `MANAGER`, `MEMBER`) |
| `activityScore` | BigDecimal | 활동 점수 |
| `createdAt` | String | 가입 일시 (형식: `yy.MM.dd HH:mm`) |
| `memberStatus` | String | 가입 상태 (`REGISTERING`, `WAITING`, `APPROVED`, `REJECTED`, `WITHDRAWN`) |
| `isActive` | Boolean | 활동 상태 여부 |
| `trackList` | Array | 트랙 정보 리스트 |
| `trackList[].generation` | Integer | 기수 |
| `trackList[].part` | String | 파트 |
| `careerList` | Array | 커리어 정보 리스트 |
| `careerList[].careerId` | Long | 커리어 ID |
| `careerList[].companyName` | String | 회사명 |
| `careerList[].position` | String | 직위/직책 |
| `careerList[].startDate` | String | 시작일 (YearMonth 형식, 예: `2024-01`) |
| `careerList[].endDate` | String | 종료일 (YearMonth 형식, null 가능) |
| `careerList[].isWorking` | Boolean | 현재 재직 여부 |

**응답 예시**

```json
{
  "code": 200,
  "message": "[관리자 페이지]에서 유저 정보를 조회합니다.",
  "data": {
    "username": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "phoneNumberPublic": true,
    "phoneNumber": "010-1234-5678",
    "selfIntroduction": "안녕하세요! 백엔드 개발자입니다.",
    "link": "https://github.com/honggildong",
    "email": "hong@example.com",
    "university": "서울과학기술대학교",
    "graduateSchool": null,
    "role": "MEMBER",
    "activityScore": 85.5,
    "createdAt": "25.01.15 14:30",
    "memberStatus": "APPROVED",
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
        "position": "백엔드 개발자",
        "startDate": "2024-01",
        "endDate": null,
        "isWorking": true
      }
    ]
  }
}
```

---

## 3. 승인된 회원 목록 조회

### 개요
APPROVED 상태의 전체 회원 목록을 기수 기준으로 조회합니다. 키워드 검색과 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/manager/approved-members`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

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
| `generation` | Integer | 기수 | O |
| `keyword` | String | 검색 키워드 | X |
| `pageSize` | Integer | 페이지 크기 (기본값: 20) | X |
| `pageNum` | Integer | 페이지 번호 (기본값: 0) | X |

**요청 예시**

```
GET /v1/manager/approved-members?generation=15
GET /v1/manager/approved-members?generation=15&keyword=홍길동&pageSize=10&pageNum=0
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `content` | Array | 승인된 회원 목록 |
| `content[].memberId` | Long | 회원 ID |
| `content[].username` | String | 회원 이름 |
| `content[].university` | String | 대학교 |
| `content[].profileImageUrl` | String | 프로필 이미지 URL |
| `content[].trackList` | Array | 트랙 정보 리스트 |
| `content[].trackList[].generation` | Integer | 기수 |
| `content[].trackList[].part` | String | 파트 |
| `content[].role` | String | 회원 역할 |
| `content[].memberStatus` | String | 가입 상태 |
| `content[].createdAt` | String | 가입 일시 (형식: `yy.MM.dd HH:mm`) |
| `pageNumber` | Integer | 현재 페이지 번호 |
| `pageSize` | Integer | 페이지 크기 |
| `numberOfElements` | Integer | 현재 페이지 요소 수 |
| `isLast` | Boolean | 마지막 페이지 여부 |

**응답 예시**

```json
{
  "code": 200,
  "message": "승인된 [전체 회원 목록]을 조회합니다.",
  "data": {
    "content": [
      {
        "memberId": 1,
        "username": "홍길동",
        "university": "서울과학기술대학교",
        "profileImageUrl": "https://example.com/profile.jpg",
        "trackList": [
          {
            "generation": 15,
            "part": "BACKEND"
          }
        ],
        "role": "MEMBER",
        "memberStatus": "APPROVED",
        "createdAt": "25.01.15 14:30"
      }
    ],
    "pageNumber": 0,
    "pageSize": 20,
    "numberOfElements": 1,
    "isLast": true
  }
}
```
