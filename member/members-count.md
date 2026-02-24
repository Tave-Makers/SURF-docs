# 멤버 상태별 회원 수 조회

## 멤버 상태별 회원 수 조회

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
