## 스크랩 추가

### 개요
특정 게시글을 스크랩합니다. 이미 스크랩된 경우에도 멱등성이 보장됩니다.

### 엔드포인트
`POST /v1/user/scraps/{postId}`

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
| postId | Long | 게시글 ID | O |

**요청 예시**
```
POST /v1/user/scraps/1
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 스크랩 추가 성공 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[스크랩]이 성공적으로 생성되었습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 게시글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```
