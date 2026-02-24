# 회원 역할 변경

## 회원 역할 변경

### 개요
관리자가 특정 회원의 역할을 변경합니다.

### 엔드포인트
`PATCH /v1/admin/members/{memberId}/role`

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
| `Content-Type` | String | `application/json` | O |

**Path Parameters**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 역할을 변경할 회원의 ID |

**Body**

| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| `role` | String | 변경할 역할 (관리자만 접근 가능 (MANAGER 이상), `MEMBER`) | O |

**요청 예시**

```json
{
  "role": "MANAGER"
}
```

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 역할 변경 성공 |

**응답 예시**

```json
{
  "code": 200,
  "message": "회원 역할이 성공적으로 변경되었습니다.",
  "data": null
}
```

---

### 실패 (Error)

| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 | Bad Request | 유효하지 않은 역할 값 |
| 404 | Not Found | 존재하지 않는 회원 |

**응답 예시 (400)**

```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```

**응답 예시 (404)**

```json
{
  "code": 404,
  "message": "존재하지 않는 [회원]입니다.",
  "data": null
}
```

---

## 사용 가능한 Role 값

| 값 | 설명 |
|----|------|
| `ADMIN` | 최고 관리자 (루트) |
| `PRESIDENT` | 회장 |
| `MANAGER` | 매니저 |
| `MEMBER` | 일반 회원 |
