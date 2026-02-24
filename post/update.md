## 게시글 수정

### 개요
본인이 작성한 게시글을 수정합니다. 작성자 본인만 수정 가능합니다.

### 엔드포인트
`PATCH /v1/user/posts/{postId}`

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

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| title | String | 수정된 제목 | O |
| content | String | 수정된 내용 | O |
| isContentChanged | Boolean | 내용 변경 여부 | X |
| categoryId | Long | 카테고리 ID | X |
| pinned | Boolean | 상단 고정 여부 | X |
| isReservationChanged | Boolean | 예약 변경 여부 | X |
| reservedAt | String | 예약 시간 (ISO 8601) | X |
| isImageChanged | Boolean | 이미지 변경 여부 | X |
| imageUrlList | Array | 변경된 이미지 목록 | X |
| imageUrlList[].originalUrl | String | 이미지 URL | O |
| imageUrlList[].sequence | Integer | 이미지 순서 | O |
| hasSchedule | Boolean | 일정 매핑 여부 | X |

**요청 예시**
```json
{
  "title": "수정된 제목",
  "content": "수정된 내용",
  "isContentChanged": true,
  "categoryId": 3,
  "pinned": false,
  "isReservationChanged": false,
  "reservedAt": null,
  "isImageChanged": true,
  "imageUrlList": [],
  "hasSchedule": false
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시글 수정 성공 |

**Body (PostDetailResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| postId | Long | 게시글 ID |
| title | String | 제목 |
| content | String | 내용 |
| pinned | Boolean | 상단 고정 여부 |
| postedAt | String | 작성 시간 (ISO 8601) |
| boardId | Long | 게시판 ID |
| categoryId | Long | 카테고리 ID |
| scrappedByMe | Boolean | 현재 사용자 스크랩 여부 |
| scrapCount | Long | 스크랩 수 |
| likedByMe | Boolean | 현재 사용자 좋아요 여부 |
| likeCount | Long | 좋아요 수 |
| commentCount | Long | 댓글 수 |
| nickname | String | 작성자 닉네임 |
| profileImageUrl | String | 작성자 프로필 이미지 URL |
| isMine | Boolean | 본인 게시글 여부 |
| imageUrlList | Array | 이미지 목록 |
| isReserved | Boolean | 예약 게시글 여부 |
| reservedAt | String | 예약 시간 |
| viewCount | Integer | 조회수 |
| hasSchedule | Boolean | 일정 매핑 여부 |
| scheduleId | Long | 일정 ID |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시글]이 성공적으로 수정되었습니다.",
  "data": {
    "postId": 1,
    "title": "수정된 제목",
    "content": "수정된 내용",
    "pinned": false,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 3,
    "scrappedByMe": false,
    "scrapCount": 5,
    "likedByMe": false,
    "likeCount": 3,
    "commentCount": 0,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": true,
    "imageUrlList": [],
    "isReserved": false,
    "reservedAt": null,
    "viewCount": 10,
    "hasSchedule": false,
    "scheduleId": null
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 권한 없음 | 작성자 본인이 아닌 경우 |
| 404 Not Found | 게시글 없음 | 해당 ID의 게시글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 401,
  "message": "[게시글]을 수정할 권한이 없습니다.",
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
