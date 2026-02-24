# 기수 정보 조회

## 기수 정보 조회

### 개요
존재하는 회원들의 모든 기수 정보를 조회합니다. 각 기수의 번호와 표시 이름(예: "15기")을 반환합니다.

### 엔드포인트
`GET /v1/user/generations`

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

파라미터 및 Body 없음.

---

### 응답 (Response)

**성공**

| HTTP Status | 의미 |
|-------------|------|
| 200 | OK - 조회 성공 |

**Body**

| Key | Type | 설명 |
|-----|------|------|
| `generations` | Array | 기수 정보 리스트 |
| `generations[].generation` | Integer | 기수 번호 |
| `generations[].name` | String | 기수 표시 이름 (예: "15기") |

**응답 예시**

```json
{
  "code": 200,
  "message": "[전체 회원수]와 회원들의 모든 [기수]를 조회합니다.",
  "data": {
    "generations": [
      {
        "generation": 13,
        "name": "13기"
      },
      {
        "generation": 14,
        "name": "14기"
      },
      {
        "generation": 15,
        "name": "15기"
      }
    ]
  }
}
```
