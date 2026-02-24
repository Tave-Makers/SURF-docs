# 회원 검색

## 회원 이름/학교 검색 (기수/파트 필터링)

### 개요
회원 이름 및 학교로 검색하며, 기수와 파트로 필터링할 수 있습니다. 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/user/members`

### 인증
- **인증 필요 여부:** 필요
- **권한:** `MEMBER`, `MANAGER`, `PRESIDENT`, `ADMIN`

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
