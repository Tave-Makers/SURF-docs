## 게시글 생성

### 개요
새로운 게시글을 생성합니다. 작성자는 현재 로그인한 사용자로 자동 지정됩니다.

### 엔드포인트
`POST /v1/user/posts`

### 인증
- **인증 필요 여부:** 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| boardId | Long | 게시판 ID | O |
| categoryId | Long | 카테고리 ID | O |
| title | String | 게시글 제목 | O |
| content | String | 게시글 내용 | O |
| pinned | Boolean | 상단 고정 여부 (기본값: false) | X |
| reservedAt | String | 예약 시간 (ISO 8601, 미래 시간만 가능) | X |
| imageUrlList | Array | 이미지 목록 | X |
| imageUrlList[].originalUrl | String | 이미지 URL | O |
| imageUrlList[].sequence | Integer | 이미지 순서 | O |
| hasSchedule | Boolean | 일정 매핑 여부 | X |

**요청 예시**
```json
{
  "boardId": 1,
  "categoryId": 2,
  "title": "만남의 장 공지사항",
  "content": "전반기 만남의 장 안내입니다.",
  "pinned": true,
  "reservedAt": null,
  "imageUrlList": [
    {
      "originalUrl": "https://s3.../image.jpg",
      "sequence": 1
    }
  ],
  "hasSchedule": false
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 게시글 생성 성공 |

**Body**
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
| imageUrlList[].imageId | Long | 이미지 ID |
| imageUrlList[].originalUrl | String | 이미지 URL |
| imageUrlList[].postId | Long | 게시글 ID |
| imageUrlList[].sequence | Integer | 이미지 순서 |
| isReserved | Boolean | 예약 게시글 여부 |
| reservedAt | String | 예약 시간 |
| viewCount | Integer | 조회수 |
| hasSchedule | Boolean | 일정 매핑 여부 |
| scheduleId | Long | 일정 ID |

**응답 예시**
```json
{
  "code": 201,
  "message": "[게시글]이 성공적으로 생성되었습니다.",
  "data": {
    "postId": 1,
    "title": "만남의 장 공지사항",
    "content": "전반기 만남의 장 안내입니다.",
    "pinned": true,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 2,
    "scrappedByMe": false,
    "scrapCount": 0,
    "likedByMe": false,
    "likeCount": 0,
    "commentCount": 0,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": true,
    "imageUrlList": [
      {
        "imageId": 1,
        "originalUrl": "https://s3.../image.jpg",
        "postId": 1,
        "sequence": 1
      }
    ],
    "isReserved": false,
    "reservedAt": null,
    "viewCount": 0,
    "hasSchedule": false,
    "scheduleId": null
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효하지 않은 입력값 | 필수 필드 누락 또는 잘못된 값 |
| 404 Not Found | 리소스 없음 | 게시판 또는 카테고리가 존재하지 않음 |

**응답 예시**
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시판]입니다.",
  "data": null
}
```
