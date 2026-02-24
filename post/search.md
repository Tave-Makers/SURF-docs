## 게시글 검색

### 개요
게시글 검색 및 최근 검색어 관리 기능을 제공합니다.

### 인증
- **인증 필요 여부:** 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

## 1. 게시글 검색

### 엔드포인트
`GET /v1/user/search/posts`

게시글을 제목과 본문 기준으로 검색합니다. 최근 검색어가 자동으로 저장됩니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| param | String | 검색어 | O |
| page | Integer | 페이지 번호 (기본값: 0) | X |
| size | Integer | 페이지 크기 (기본값: 20) | X |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 검색 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array | 검색 결과 목록 (PostResDTO) |
| hasNext | Boolean | 다음 페이지 존재 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "검색이 성공적으로 완료되었습니다.",
  "data": {
    "content": [
      {
        "postId": 5,
        "title": "검색된 게시글",
        "content": "검색어가 포함된 내용...",
        "pinned": false,
        "postedAt": "2025-10-03T10:00:00",
        "thumbnailImageUrl": "https://s3.../thumb.jpg",
        "boardId": 1,
        "categoryId": 2,
        "scrappedByMe": false,
        "scrapCount": 3,
        "likedByMe": false,
        "likeCount": 2,
        "commentCount": 1,
        "nickname": "사용자",
        "isReserved": false,
        "viewCount": 45
      }
    ],
    "hasNext": false
  }
}
```

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 검색어 누락 | 검색어가 입력되지 않음 |

**응답 예시**
```json
{
  "code": 400,
  "message": "검색어를 입력해주세요",
  "data": null
}
```

---

## 2. 최근 검색어 조회

### 엔드포인트
`GET /v1/user/search/recent`

현재 사용자의 최근 검색어 10개를 최신순으로 조회합니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "최근 검색어 목록이 성공적으로 조회되었습니다.",
  "data": ["검색어1", "검색어2", "검색어3"]
}
```

---

## 3. 최근 검색어 전체 삭제

### 엔드포인트
`DELETE /v1/user/search/recent`

현재 사용자의 모든 최근 검색어를 삭제합니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "최근 검색어가 성공적으로 삭제되었습니다.",
  "data": null
}
```

---

## 4. 최근 검색어 단건 삭제

### 엔드포인트
`DELETE /v1/user/search/recent/{keyword}`

특정 최근 검색어 하나를 삭제합니다.

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 액세스 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| keyword | String | 삭제할 검색어 | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

**응답 예시**
```json
{
  "code": 204,
  "message": "최근 검색어 한 개가 성공적으로 삭제되었습니다.",
  "data": null
}
```
