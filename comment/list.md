## 댓글 목록 조회

### 개요
특정 게시글의 루트 댓글과 대댓글을 페이징하여 조회합니다.

### 엔드포인트
`GET /v1/user/posts/{postId}/comments`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

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

**Query Parameters**
| Key | Type | 설명 | 필수 | 기본값 |
|-----|------|------|------|--------|
| page | Integer | 페이지 번호 | X | 0 |
| size | Integer | 페이지 크기 | X | 10 |
| sort | String | 정렬 기준 | X | createdAt,desc |

**요청 예시**
```
GET /v1/user/posts/3/comments?page=0&size=10&sort=createdAt,desc
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| comments | Array | 댓글 목록 |
| comments[].id | Long | 댓글 ID |
| comments[].postId | Long | 게시글 ID |
| comments[].rootId | Long | 루트 댓글 ID |
| comments[].parentId | Long | 부모 댓글 ID (루트면 null) |
| comments[].depth | Integer | 댓글 깊이 (0=루트) |
| comments[].content | String | 댓글 내용 |
| comments[].memberId | Long | 작성자 회원 ID |
| comments[].nickname | String | 작성자 닉네임 |
| comments[].profileImageUrl | String | 작성자 프로필 이미지 URL |
| comments[].likeCount | Long | 좋아요 수 |
| comments[].liked | Boolean | 현재 사용자 좋아요 여부 |
| comments[].createdAt | String | 작성일시 |
| comments[].mentions | Array | 멘션된 회원 목록 |
| comments[].mentions[].memberId | Long | 멘션된 회원 ID |
| comments[].mentions[].nickname | String | 멘션된 회원 닉네임 |
| totalCount | Long | 전체 댓글 수 |
| hasNext | Boolean | 다음 페이지 존재 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글]이 성공적으로 조회되었습니다.",
  "data": {
    "comments": [
      {
        "id": 15,
        "postId": 3,
        "rootId": 15,
        "parentId": null,
        "depth": 0,
        "content": "좋은 공지 감사합니다!",
        "memberId": 7,
        "nickname": "민수",
        "profileImageUrl": "https://example.com/profile.jpg",
        "likeCount": 2,
        "liked": false,
        "createdAt": "2025-02-24T10:30:00",
        "mentions": [
          {
            "memberId": 5,
            "nickname": "홍길동"
          }
        ]
      },
      {
        "id": 16,
        "postId": 3,
        "rootId": 15,
        "parentId": 15,
        "depth": 1,
        "content": "동의합니다!",
        "memberId": 5,
        "nickname": "홍길동",
        "profileImageUrl": "https://example.com/profile2.jpg",
        "likeCount": 1,
        "liked": true,
        "createdAt": "2025-02-24T11:00:00",
        "mentions": [
          {
            "memberId": 7,
            "nickname": "민수"
          }
        ]
      }
    ],
    "totalCount": 37,
    "hasNext": true
  }
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
