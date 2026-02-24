## 게시판 생성

### 개요
새로운 게시판을 생성합니다. 관리자 권한이 필요합니다.

### 엔드포인트
`POST /v1/admin/boards`

### 인증
- **인증 필요 여부:** 필요
- **권한:** `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| name | String | 게시판 이름 (공백 불가) | O |
| type | String | 게시판 타입 (`NOTICE`) | O |

**요청 예시**
```json
{
  "name": "공지사항",
  "type": "NOTICE"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 게시판 생성 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| id | Long | 게시판 ID |
| name | String | 게시판 이름 |
| type | String | 게시판 타입 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[게시판]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 1,
    "name": "공지사항",
    "type": "NOTICE"
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효하지 않은 입력값 | 필수 필드 누락 또는 잘못된 값 |

**응답 예시**
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
