## 게시글 첨부파일 삭제

### 개요
게시글 첨부파일 삭제

### 엔드포인트
`DELETE /v1/user/posts/{postId}/files/{fileId}`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

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
| postId | Long | postId | O |
| fileId | Long | fileId | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 요청 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
