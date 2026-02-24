# 온보딩 상태 확인

## 온보딩(추가 정보 입력) 필요 여부 확인

### 개요
카카오 로그인 후 추가 정보 입력이 필요한 상태인지 확인합니다. 회원의 현재 상태(MemberStatus)와 역할(MemberRole)을 반환합니다.

### 엔드포인트
`GET /v1/user/members/valid-status`

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

파라미터 및 Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 상태 확인 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `memberId` | Long | 회원 ID |
| `needOnboarding` | Boolean | 추가 정보 입력 필요 여부 |
| `memberStatus` | String | 회원 상태 (MemberStatus Enum 참조) |
| `memberRole` | String | 회원 역할 (MemberRole Enum 참조) |

**응답 예시**

```json
{
  "code": 200,
  "message": "[회원]의 추가 회원가입 정보 입력 필요 여부를 확인했습니다.",
  "data": {
    "memberId": 1,
    "needOnboarding": true,
    "memberStatus": "REGISTERING",
    "memberRole": "MEMBER"
  }
}
```

---

## MemberStatus Enum

| 값 | 설명 |
|----|------|
| `REGISTERING` | 가입 중 (추가 정보 입력 필요) |
| `WAITING` | 승인 대기 중 |
| `APPROVED` | 승인됨 |
| `REJECTED` | 거절됨 |
| `WITHDRAWN` | 탈퇴됨 |

## MemberRole Enum

| 값 | 설명 |
|----|------|
| `ADMIN` | 최고 관리자 (루트) |
| `PRESIDENT` | 회장 |
| `MANAGER` | 매니저 |
| `MEMBER` | 일반 회원 |
