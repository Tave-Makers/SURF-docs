# 이름 기반 회원 조회

## 이름 기반 회원 조회

### 개요
관리자가 이름으로 활동 중인 회원을 검색합니다. 트랙 및 기수 정보와 함께 반환됩니다.

### 엔드포인트
`GET /v1/admin/members/search`

### 인증
- **인증 필요 여부:** 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

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
| `name` | String | 검색할 회원 이름 | O |

**요청 예시**

```
GET /v1/admin/members/search?name=홍길동
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body (Array)**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 회원 ID |
| `name` | String | 회원 이름 |
| `generation` | Integer | 참여 기수 |
| `track` | String | 참여 트랙(파트) |

**응답 예시**

```json
{
  "code": 200,
  "message": "'홍길동'(으)로 활동 중인 [회원]을 조회했습니다.",
  "data": [
    {
      "memberId": 1,
      "name": "홍길동",
      "generation": 15,
      "track": "백엔드"
    }
  ]
}
```
