## 내 스크랩 목록

### 개요
본인이 스크랩한 게시글 목록을 조회합니다.

### 엔드포인트
`GET /v1/user/scraps/me`

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

**Query Parameters**
| Key | Type | 설명 | 필수 | 기본값 |
|-----|------|------|------|--------|
| page | Integer | 페이지 번호 | X | 0 |
| size | Integer | 페이지 크기 | X | 12 |

**요청 예시**
```
GET /v1/user/scraps/me?page=0&size=12
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body (Slice\<PostResDTO\>)**
| Key | Type | 설명 |
|-----|------|------|
| postId | Long | 게시글 ID |
| title | String | 게시글 제목 |
| content | String | 게시글 내용 |
| pinned | Boolean | 고정 여부 |
| postedAt | String | 게시일시 |
| thumbnailImageUrl | String | 썸네일 이미지 URL |
| boardId | Long | 게시판 ID |
| categoryId | Long | 카테고리 ID |
| scrappedByMe | Boolean | 본인 스크랩 여부 |
| scrapCount | Integer | 스크랩 수 |
| likedByMe | Boolean | 본인 좋아요 여부 |
| likeCount | Integer | 좋아요 수 |
| commentCount | Integer | 댓글 수 |
| nickname | String | 작성자 닉네임 |
| isReserved | Boolean | 예약 게시글 여부 |
| viewCount | Integer | 조회수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[스크랩] 목록이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "postId": 1,
        "title": "만남의 장 공지사항",
        "content": "전반기 만남의 장 안내입니다.",
        "pinned": true,
        "postedAt": "2025-10-05T14:48:00",
        "thumbnailImageUrl": "https://s3.../thumb.jpg",
        "boardId": 1,
        "categoryId": 2,
        "scrappedByMe": true,
        "scrapCount": 10,
        "likedByMe": true,
        "likeCount": 5,
        "commentCount": 0,
        "nickname": "홍길동",
        "isReserved": false,
        "viewCount": 100
      }
    ],
    "last": true,
    "numberOfElements": 1
  }
}
```
