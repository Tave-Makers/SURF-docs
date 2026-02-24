## 댓글 좋아요

### 개요
댓글에 대한 좋아요 토글, 개수 조회, 본인 좋아요 여부 조회, 좋아요 누른 회원 목록 조회 기능을 제공합니다.

### 인증 (공통)
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

### 1. 좋아요 토글

#### 엔드포인트
`POST /v1/user/comments/{commentId}/like`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| commentId | Long | 댓글 ID | O |

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 토글 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| liked | Boolean | 좋아요 상태 (true: 좋아요, false: 취소) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 상태가 성공적으로 변경되었습니다.",
  "data": {
    "liked": true
  }
}
```

#### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 댓글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [댓글]입니다.",
  "data": null
}
```

---

### 2. 좋아요 개수 조회

#### 엔드포인트
`GET /v1/user/comments/{commentId}/like/count`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| commentId | Long | 댓글 ID | O |

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| data | Integer | 좋아요 개수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 개수가 성공적으로 조회되었습니다.",
  "data": 5
}
```

---

### 3. 본인 좋아요 여부 조회

#### 엔드포인트
`GET /v1/user/comments/{commentId}/like/me`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| commentId | Long | 댓글 ID | O |

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| data | Boolean | 본인 좋아요 여부 (true/false) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 상태가 성공적으로 조회되었습니다.",
  "data": true
}
```

---

### 4. 좋아요 누른 회원 목록

#### 엔드포인트
`GET /v1/user/comments/{commentId}/like/members`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| commentId | Long | 댓글 ID | O |

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| memberId | Long | 회원 ID |
| nickname | String | 닉네임 |
| profileImageUrl | String | 프로필 이미지 URL |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 누른 회원 목록이 성공적으로 조회되었습니다.",
  "data": [
    {
      "memberId": 5,
      "nickname": "홍길동",
      "profileImageUrl": "https://example.com/profile.jpg"
    }
  ]
}
```
