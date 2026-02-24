# 게시판 단건 조회

## 게시판 단건 조회 (관리자)

### 엔드포인트
`GET /v1/admin/boards/{boardId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| boardId | Long | 게시판 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| id | Long | 게시판 ID |
| name | String | 게시판 이름 |
| type | String | 게시판 타입 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시판]이 성공적으로 조회되었습니다.",
  "data": {
    "id": 1,
    "name": "공지사항",
    "type": "NOTICE"
  }
}
```

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 게시판 없음 | 해당 ID의 게시판이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시판]입니다.",
  "data": null
}
```
