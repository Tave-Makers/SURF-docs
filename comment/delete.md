## 댓글 삭제

### 개요
본인이 작성한 댓글을 삭제합니다. Hard 삭제 처리됩니다.

### 엔드포인트
`DELETE /v1/user/posts/{postId}/comments/{commentId}`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `MEMBER` (본인 댓글만 삭제 가능)

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
| postId | Long | 게시글 ID | O |
| commentId | Long | 댓글 ID | O |

**요청 예시**
```
DELETE /v1/user/posts/3/comments/15
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "[댓글]이 성공적으로 삭제되었습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 403 Forbidden | 권한 없음 | 본인의 댓글이 아님 |
| 404 Not Found | 리소스 없음 | 댓글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 403,
  "message": "본인의 [댓글]이 아닙니다.",
  "data": null
}
```

```json
{
  "code": 404,
  "message": "존재하지 않는 [댓글]입니다.",
  "data": null
}
```
