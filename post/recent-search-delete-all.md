## 최근 검색어 전체 삭제

### 개요
현재 사용자의 모든 최근 검색어를 삭제합니다.

### 인증
- **인증 필요 여부:** 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

### 엔드포인트
`DELETE /v1/user/search/recent`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "최근 검색어가 성공적으로 삭제되었습니다.",
  "data": null
}
```
