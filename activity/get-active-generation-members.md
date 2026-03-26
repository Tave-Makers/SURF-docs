## 현재 활동 기수에 속한 회원 조회

### 개요
현재 활동 기수에 속한 회원 조회

### 엔드포인트
`GET /v1/manager/active-generation/members`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 요청 성공 |

**Body (List<ActiveGenerationMemberResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| - | List<ActiveGenerationMemberResDTO | 응답 데이터 |

**응답 예시**
```json
{
  "code": 200,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
