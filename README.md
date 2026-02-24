# SURF API Documentation

SURF는 TAVE 동아리 운영을 위한 커뮤니티 플랫폼입니다.

## Base URL

| 환경 | URL |
|------|-----|
| Production | `https://tavesurf.site` |
| Local | `http://localhost:8080` |

## 인증 방식

SURF API는 **JWT (JSON Web Token)** 기반 인증을 사용합니다.

### Access Token
- 모든 인증이 필요한 API 요청 시 `Authorization` 헤더에 포함
- 형식: `Authorization: Bearer {accessToken}`
- 만료 시간: 1시간

### Refresh Token
- HttpOnly 쿠키로 자동 관리
- 만료 시간: 14일
- Refresh Token Rotation (RTR) 적용

## 권한 체계

| 권한 | 설명 | 접근 가능 경로 |
|------|------|--------------|
| MEMBER | 일반 회원 | `/v1/user/**` |
| MANAGER | 매니저 | `/v1/user/**`, `/v1/admin/**` |
| PRESIDENT | 회장 | `/v1/user/**`, `/v1/admin/**` |
| ADMIN | 관리자 (루트) | `/v1/user/**`, `/v1/admin/**` |

## 공통 응답 형식

### 성공 응답
```json
{
  "code": 200,
  "message": "성공 메시지",
  "data": { }
}
```

### 에러 응답
```json
{
  "code": 400,
  "message": "에러 메시지",
  "data": null
}
```

### 유효성 검증 실패 응답
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": [
    {
      "errorField": "email",
      "errorMessage": "올바른 이메일 형식이어야 합니다",
      "inputValue": "invalid-email"
    }
  ]
}
```

## 공통 HTTP Status Code

| Status | 설명 |
|--------|------|
| 200 | OK - 요청 성공 |
| 201 | Created - 리소스 생성 성공 |
| 204 | No Content - 삭제 성공 |
| 400 | Bad Request - 입력값 오류 |
| 401 | Unauthorized - 인증 실패 |
| 403 | Forbidden - 권한 부족 |
| 404 | Not Found - 리소스 없음 |
| 409 | Conflict - 리소스 충돌 |
| 429 | Too Many Requests - 요청 한도 초과 |
| 500 | Internal Server Error - 서버 오류 |

## CORS 설정

**허용 Origin:**
- `http://localhost:3000`
- `http://localhost:5173`
- `https://tavesurf.site`

**허용 Method:** GET, POST, PATCH, PUT, DELETE, OPTIONS
