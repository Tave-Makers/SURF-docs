## 게시글 삭제

### 개요
본인이 작성한 게시글을 삭제합니다. 작성자 본인만 삭제 가능합니다.

### 엔드포인트
`DELETE /v1/user/posts/{postId}`

### 인증
- **인증 필요 여부:** 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상, 작성자 본인만)

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
| postId | Long | 게시글 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 게시글 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "[게시글]이 성공적으로 삭제되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 권한 없음 | 작성자 본인이 아닌 경우 |
| 404 Not Found | 게시글 없음 | 해당 ID의 게시글이 존재하지 않음 또는 이미 삭제됨 |

**응답 예시**
```json
{
  "code": 401,
  "message": "[게시글]을 삭제할 권한이 없습니다.",
  "data": null
}
```
```json
{
  "code": 404,
  "message": "이미 삭제된 [게시글]입니다.",
  "data": null
}
```
