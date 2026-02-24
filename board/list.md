## 게시판 목록 조회

### 개요
모든 게시판 목록을 조회합니다.

### 엔드포인트
`GET /v1/user/boards`

### 인증
- **인증 필요 여부:** 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시판 목록 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| [] | Array | 게시판 목록 배열 |
| [].id | Long | 게시판 ID |
| [].name | String | 게시판 이름 |
| [].type | String | 게시판 타입 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시판]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 1,
      "name": "공지사항",
      "type": "NOTICE"
    },
    {
      "id": 2,
      "name": "자유게시판",
      "type": "NOTICE"
    }
  ]
}
```
