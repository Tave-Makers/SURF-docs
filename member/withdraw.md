# 회원 탈퇴

## 회원 탈퇴

### 개요
로그인한 사용자가 회원 탈퇴를 요청합니다. 탈퇴 처리 후 Refresh Token 쿠키가 삭제됩니다.

### 엔드포인트
`POST /v1/user/members/withdraw`

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

Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 204 | No Content - 회원 탈퇴 완료 |

**응답 예시**

```json
{
  "code": 204,
  "message": "회원 탈퇴 완료",
  "data": null
}
```

---

### 참고사항
- 탈퇴 시 서버에서 Refresh Token 쿠키를 자동으로 삭제합니다.
- 탈퇴 후에는 동일 계정으로 다시 로그인할 수 없습니다.
