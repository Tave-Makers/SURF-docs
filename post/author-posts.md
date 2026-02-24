## 특정 작성자의 게시글 조회

### 개요
특정 작성자가 작성한 게시글 목록을 조회합니다.

### 인증
- **인증 필요 여부:** 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

### 엔드포인트
`GET /v1/user/posts/author/{authorId}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| authorId | Long | 작성자 회원 ID | O |

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| page | Integer | 페이지 번호 (기본값: 0) | X |
| size | Integer | 페이지 크기 (기본값: 12) | X |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "특정 회원이 작성한 [게시글] 목록을 성공적으로 조회했습니다.",
  "data": {
    "content": [...],
    "hasNext": false
  }
}
```

---

### 목록 Response 필드 (PostResDTO)

| Key | Type | 설명 |
|-----|------|------|
| postId | Long | 게시글 ID |
| title | String | 제목 |
| content | String | 내용 |
| pinned | Boolean | 상단 고정 여부 |
| postedAt | String | 작성 시간 (ISO 8601) |
| thumbnailImageUrl | String | 썸네일 이미지 URL |
| boardId | Long | 게시판 ID |
| categoryId | Long | 카테고리 ID |
| scrappedByMe | Boolean | 현재 사용자 스크랩 여부 |
| scrapCount | Long | 스크랩 수 |
| likedByMe | Boolean | 현재 사용자 좋아요 여부 |
| likeCount | Long | 좋아요 수 |
| commentCount | Long | 댓글 수 |
| nickname | String | 작성자 닉네임 |
| isReserved | Boolean | 예약 게시글 여부 |
| viewCount | Integer | 조회수 |
