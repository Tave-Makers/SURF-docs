## 배지 목록 조회

### 개요
배지 목록 조회

### 엔드포인트
`GET /v1/admin/badges`

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

**Query Parameters**
| Key | Type | 설명 | 필수 | 기본값 |
|-----|------|------|------|--------|
| page | Integer | page | O | - |
| size | Integer | size | O | - |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 요청 성공 |

**Body (BadgeSliceResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| content | List<BadgeResDTO> | content |
| pageNumber | Integer | pageNumber |
| pageSize | Integer | pageSize |
| hasNext | Boolean | hasNext |

**응답 예시**
```json
{
  "code": 200,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
