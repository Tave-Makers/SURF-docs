# SURF API Documentation

## 소개

SURF는 TAVE 동아리 운영을 위한 백엔드 API 서비스입니다. 이 문서는 SURF API의 사용 방법과 규격을 정리한 것입니다.

---

## Base URL

| 환경 | URL |
|------|-----|
| Production | `https://tavesurf.site` |
| Local | `http://localhost:8080` |

---

## 인증 방식

SURF API는 JWT(JSON Web Token) 기반 Bearer Token 인증을 사용합니다.

### Token 종류

| Token | 유효 기간 | 전달 방식 | 설명 |
|-------|-----------|-----------|------|
| Access Token | 1시간 | Authorization Header | API 요청 시 인증에 사용 |
| Refresh Token | 14일 | HttpOnly Cookie | Access Token 재발급에 사용 |

### 인증 헤더

인증이 필요한 API 요청 시, HTTP 헤더에 다음과 같이 Access Token을 포함해야 합니다.

```
Authorization: Bearer {ACCESS_TOKEN}
```

### Token 재발급

Access Token이 만료된 경우, `POST /auth/refresh` 엔드포인트를 통해 Refresh Token 쿠키를 이용하여 새로운 Access Token을 발급받을 수 있습니다. Refresh Token Rotation(RTR) 방식이 적용되어, 재발급 시 Refresh Token도 함께 갱신됩니다.

---

## 권한 체계

SURF API는 역할 기반 접근 제어(RBAC)를 사용합니다.

### 역할(Role) 목록

| 역할 | 설명 |
|------|------|
| `ADMIN` | 최고 관리자 (루트) |
| `PRESIDENT` | 회장 |
| `MANAGER` | 매니저 |
| `MEMBER` | 일반 회원 |

### 접근 권한 범위

| 경로 패턴 | 접근 가능 역할 |
|-----------|---------------|
| `/v1/user/**` | `MEMBER`, `MANAGER`, `PRESIDENT`, `ADMIN` |
| `/v1/admin/**` | `MANAGER`, `PRESIDENT`, `ADMIN` |

---

## 공통 응답 형식

모든 API 응답은 아래의 공통 형식을 따릅니다.

### 성공 응답

```json
{
  "code": 200,
  "message": "요청 성공 메시지",
  "data": { ... }
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
  "message": "유효성 검증 실패 메시지",
  "data": null
}
```

---

## HTTP Status Code

| Status Code | 의미 | 설명 |
|-------------|------|------|
| 200 | OK | 요청 성공 |
| 201 | Created | 리소스 생성 성공 |
| 204 | No Content | 요청 성공 (응답 본문 없음) |
| 302 | Found | 리다이렉트 |
| 400 | Bad Request | 잘못된 요청 또는 유효성 검증 실패 |
| 401 | Unauthorized | 인증 실패 또는 토큰 만료 |
| 403 | Forbidden | 접근 권한 없음 |
| 404 | Not Found | 리소스를 찾을 수 없음 |
| 409 | Conflict | 리소스 충돌 (이미 존재하는 데이터 등) |
| 500 | Internal Server Error | 서버 내부 오류 |
