## 댓글 생성

### 개요
루트 댓글 또는 대댓글을 생성합니다. 대댓글은 `parentId`를 지정하며, 부모 댓글 작성자를 멘션해야 합니다.

### 엔드포인트
`POST /v1/user/posts/{postId}/comments`

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

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| parentId | Long | 부모 댓글 ID (대댓글일 때만, 루트 댓글은 null) | X |
| content | String | 댓글 내용 (최대 1000자) | O |
| mentionMemberIds | Array\<Long\> | 멘션할 회원 ID 목록 | X |

**요청 예시 (루트 댓글)**
```json
{
  "parentId": null,
  "content": "좋은 글이네요!",
  "mentionMemberIds": []
}
```

**요청 예시 (대댓글)**
```json
{
  "parentId": 15,
  "content": "동의합니다!",
  "mentionMemberIds": [7]
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 댓글 생성 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| id | Long | 댓글 ID |
| postId | Long | 게시글 ID |
| rootId | Long | 루트 댓글 ID |
| parentId | Long | 부모 댓글 ID (루트면 null) |
| depth | Integer | 댓글 깊이 (0=루트) |
| content | String | 댓글 내용 |
| memberId | Long | 작성자 회원 ID |
| nickname | String | 작성자 닉네임 |
| profileImageUrl | String | 작성자 프로필 이미지 URL |
| likeCount | Long | 좋아요 수 |
| liked | Boolean | 현재 사용자 좋아요 여부 |
| createdAt | String | 작성일시 |
| mentions | Array | 멘션된 회원 목록 |
| mentions[].memberId | Long | 멘션된 회원 ID |
| mentions[].nickname | String | 멘션된 회원 닉네임 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[댓글]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 15,
    "postId": 3,
    "rootId": 15,
    "parentId": null,
    "depth": 0,
    "content": "좋은 공지 감사합니다!",
    "memberId": 7,
    "nickname": "민수",
    "profileImageUrl": "https://example.com/profile.jpg",
    "likeCount": 0,
    "liked": false,
    "createdAt": "2025-02-24T10:30:00",
    "mentions": [
      {
        "memberId": 5,
        "nickname": "홍길동"
      }
    ]
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효성 검증 실패 | 공백 댓글, 대댓글 멘션 규칙 위반, 자기 멘션 |
| 404 Not Found | 리소스 없음 | 게시글 또는 부모 댓글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 400,
  "message": "[댓글] 내용은 공백일 수 없습니다.",
  "data": null
}
```

```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```

---

### 대댓글 멘션 규칙

- 대댓글 작성 시 부모 댓글 작성자를 반드시 `mentionMemberIds`에 포함해야 합니다.
- 예외: 본인 댓글에 대한 대댓글은 자기 멘션 검증을 스킵합니다.
- 자기 자신을 멘션할 수 없습니다.
