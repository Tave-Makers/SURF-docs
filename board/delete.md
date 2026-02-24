## 게시판 삭제

### 개요
특정 게시판을 삭제합니다. 관리자 권한이 필요합니다.

### 엔드포인트
`DELETE /v1/admin/boards/{boardId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| boardId | Long | 게시판 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 게시판 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "[게시판]이 성공적으로 삭제되었습니다."
}
```

---

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
