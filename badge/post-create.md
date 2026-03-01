## 배지 생성

### 개요
배지 생성

### 엔드포인트
`POST /v1/admin/badges`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Body (BadgeCreateReqDTO)**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| name | String | name | X |
| imageUrl | String | imageUrl | X |
| description | String | description | X |
| requirement | String | requirement | X |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 요청 성공 |

**응답 예시**
```json
{
  "code": 201,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
