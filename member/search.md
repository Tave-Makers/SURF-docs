# 회원 검색

## 1. 회원 이름/학교 검색 (기수/파트 필터링)

### 개요
회원 이름 및 학교로 검색하며, 기수와 파트로 필터링할 수 있습니다. 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/user/members`

### 인증
- **인증 필요 여부:** JWT 인증 필요
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
| `pageNum` | Integer | 페이지 번호 (0부터 시작) | O |
| `pageSize` | Integer | 페이지 크기 | O |
| `keyword` | String | 검색 키워드 (이름 또는 학교) | X |
| `generation` | Integer | 기수 필터 | X |
| `part` | String | 파트 필터 (Part Enum 값) | X |

**요청 예시**

```
GET /v1/user/members?pageNum=0&pageSize=10
GET /v1/user/members?pageNum=0&pageSize=10&keyword=홍길동&generation=15&part=BACKEND
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 검색 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `content` | Array | 회원 목록 |
| `content[].memberId` | Long | 회원 ID |
| `content[].username` | String | 회원 이름 |
| `content[].university` | String | 대학교 |
| `content[].selfIntroduction` | String | 자기소개 |
| `content[].profileImageUrl` | String | 프로필 이미지 URL |
| `content[].role` | String | 회원 역할 |
| `content[].trackList` | Array | 트랙 정보 리스트 |
| `content[].trackList[].generation` | Integer | 기수 |
| `content[].trackList[].part` | String | 파트 |
| `totalCount` | Long | 전체 결과 수 |
| `pageNumber` | Integer | 현재 페이지 번호 |
| `pageSize` | Integer | 페이지 크기 |
| `numberOfElements` | Integer | 현재 페이지 요소 수 |
| `isLast` | Boolean | 마지막 페이지 여부 |

**응답 예시**

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

---

## 2. 멤버 상태별 회원 수 조회

### 개요
멤버 상태(MemberStatus)에 따른 전체 회원 수를 조회합니다. 여러 상태를 동시에 지정할 수 있으며, 키워드 검색과 함께 사용할 수 있습니다.

### 엔드포인트
`GET /v1/user/members-count`

### 인증
- **인증 필요 여부:** JWT 인증 필요
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
| `memberStatuses` | List\<String\> | 조회할 멤버 상태 목록 (`REGISTERING`, `WAITING`, `APPROVED`, `REJECTED`, `WITHDRAWN`) | O |
| `keyword` | String | 검색 키워드 | X |

**요청 예시**

```
GET /v1/user/members-count?memberStatuses=APPROVED
GET /v1/user/members-count?memberStatuses=APPROVED,WAITING&keyword=홍길동
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
| `appliedMemberStatus` | Array\<String\> | 적용된 멤버 상태 목록 |
| `membersCount` | Long | 해당 상태의 회원 수 |

**응답 예시**

```json
{
  "code": 200,
  "message": "[멤버 상태]에 따른 [회원 수]를 조회합니다.",
  "data": {
    "appliedMemberStatus": ["APPROVED"],
    "membersCount": 42
  }
}
```

---

## 3. 기수 정보 조회

### 개요
존재하는 회원들의 모든 기수 정보를 조회합니다. 각 기수의 번호와 표시 이름(예: "15기")을 반환합니다.

### 엔드포인트
`GET /v1/user/generations`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `Authorization` | String | `Bearer {accessToken}` | O |

파라미터 및 Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `generations` | Array | 기수 정보 리스트 |
| `generations[].generation` | Integer | 기수 번호 |
| `generations[].name` | String | 기수 표시 이름 (예: "15기") |

**응답 예시**

```json
{
  "code": 200,
  "message": "[전체 회원수]와 회원들의 모든 [기수]를 조회합니다.",
  "data": {
    "generations": [
      {
        "generation": 13,
        "name": "13기"
      },
      {
        "generation": 14,
        "name": "14기"
      },
      {
        "generation": 15,
        "name": "15기"
      }
    ]
  }
}
```
