## 게시글 좋아요

### 개요
게시글에 대한 좋아요 설정, 해제, 목록 조회 기능을 제공합니다.

### 인증
- **인증 필요 여부:** 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

## 1. 좋아요 설정

### 엔드포인트
`POST /v1/user/posts/{postId}/like`

게시글에 좋아요를 설정합니다. 멱등성이 보장됩니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| postId | Long | 게시글 ID | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 좋아요 설정 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시글] 좋아요가 성공적으로 추가되었습니다.",
  "data": null
}
```

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 게시글 없음 | 해당 ID의 게시글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```

---

## 2. 좋아요 해제

### 엔드포인트
`DELETE /v1/user/posts/{postId}/like`

게시글의 좋아요를 취소합니다. 멱등성이 보장됩니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| postId | Long | 게시글 ID | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 좋아요 해제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "[게시글] 좋아요가 성공적으로 취소되었습니다.",
  "data": null
}
```

---

## 3. 좋아요 목록 조회

### 엔드포인트
`GET /v1/user/posts/{postId}/like`

특정 게시글에 좋아요를 누른 사용자 목록을 조회합니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| postId | Long | 게시글 ID | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| likes | Array | 좋아요 사용자 목록 |
| likes[].id | Long | 사용자 ID |
| likes[].name | String | 사용자 이름 |
| likes[].profileImageUrl | String | 프로필 이미지 URL |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시글] 좋아요 리스트가 성공적으로 조회되었습니다.",
  "data": {
    "likes": [
      {
        "id": 2,
        "name": "김길동",
        "profileImageUrl": "https://example.com/profile2.jpg"
      }
    ]
  }
}
```
