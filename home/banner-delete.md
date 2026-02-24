## 배너 삭제

### 개요
특정 배너를 삭제합니다.

### 엔드포인트
`DELETE /v1/admin/home/banners/{bannerId}`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | Y |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| bannerId | Long | 배너 ID | Y |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 배너 없음 | 해당 배너를 찾을 수 없음 |
