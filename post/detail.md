## 게시글 조회

### 개요
특정 게시글의 상세 정보를 조회합니다. 스크랩/좋아요 여부는 현재 로그인 사용자 기준입니다.

### 엔드포인트
`GET /v1/user/posts/{postId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| postId | Long | 게시글 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시글 조회 성공 |

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
  "code": 200,
  "message": "[게시글]이 성공적으로 조회되었습니다.",
  "data": {
    "postId": 1,
    "title": "만남의 장 공지사항",
    "content": "전반기 만남의 장 안내입니다.",
    "pinned": true,
    "postedAt": "2025-10-05T14:48:00",
    "boardId": 1,
    "categoryId": 2,
    "scrappedByMe": true,
    "scrapCount": 10,
    "likedByMe": true,
    "likeCount": 5,
    "commentCount": 3,
    "nickname": "홍길동",
    "profileImageUrl": "https://example.com/profile.jpg",
    "isMine": false,
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
    "viewCount": 150,
    "hasSchedule": false,
    "scheduleId": null
  }
}
```

---

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
