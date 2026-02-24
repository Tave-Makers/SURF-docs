# 회원가입 승인

## 회원가입 승인

### 개요
관리자가 회원의 회원가입 요청을 승인합니다.

### 엔드포인트
`PATCH /v1/admin/members/{memberId}/approve`

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

**Path Parameters**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 승인할 회원의 ID |

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 승인 성공 |

**응답 예시**

```json
{
  "code": 200,
  "message": "승인되었습니다.",
  "data": null
}
```

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 | Not Found | 존재하지 않는 회원 |

**응답 예시 (404)**

```json
{
  "code": 404,
  "message": "존재하지 않는 [회원]입니다.",
  "data": null
}
```
