## 게시글 일정 조회

### 개요
특정 게시글에 매핑된 일정을 조회합니다.

### 엔드포인트
`GET /v1/user/post/{postId}/schedule`

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

**요청 예시**
```
GET /v1/user/post/12/schedule
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시글 일정 조회 성공 |

**Body (ScheduleResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| scheduleId | Long | 일정 ID |
| category | String | 일정 카테고리 |
| title | String | 일정 제목 |
| startAt | String | 시작 시간 (ISO 8601) |
| endAt | String | 종료 시간 (ISO 8601) |
| location | String | 장소 |
| mappedByPost | Boolean | 게시글 연동 여부 |
| postId | Long | 연동 게시글 ID (없으면 null) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[게시글]과 매핑된 [일정]이 성공적으로 조회되었습니다.",
  "data": {
    "scheduleId": 5,
    "category": "정규행사",
    "title": "만남의 장",
    "startAt": "2025-11-15T14:00:00",
    "endAt": "2025-11-15T16:00:00",
    "location": "세종대학교 광개토대왕관",
    "mappedByPost": true,
    "postId": 12
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 해당 게시글에 연동된 일정이 없음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [일정]입니다.",
  "data": null
}
```

---

---

## 게시글 일정 생성

### 개요
공지사항 게시글 작성 시 일정을 생성하고 게시글에 매핑합니다.

### 엔드포인트
`POST /v1/admin/posts/{postId}/schedules`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

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

**Body (ScheduleCreateReqDTO)**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| category | String | 일정 카테고리 | O |
| title | String | 일정 제목 | O |
| startAt | String | 시작 시간 (ISO 8601) | O |
| endAt | String | 종료 시간 (ISO 8601) | O |
| location | String | 장소 | O |

**요청 예시**
```json
{
  "category": "정규행사",
  "title": "만남의 장",
  "startAt": "2025-11-15T14:00:00",
  "endAt": "2025-11-15T16:00:00",
  "location": "세종대학교 광개토대왕관"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 게시글 일정 생성 성공 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[일정]이 성공적으로 생성되었습니다"
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 게시글이 존재하지 않음 |
| 400 Bad Request | 잘못된 요청 | 시작 시간이 종료 시간 이후인 경우 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [게시글]입니다.",
  "data": null
}
```
```json
{
  "code": 400,
  "message": "시작 시간이 종료 시간보다 이후일 수 없습니다.",
  "data": null
}
```

---

---

## 게시글 매핑 일정 삭제

### 개요
게시글에 매핑된 일정을 삭제합니다. 일정 삭제와 함께 게시글의 hasSchedule을 false로, scheduleId를 null로 업데이트합니다.

### 엔드포인트
`DELETE /v1/admin/posts/{postId}/schedules/{scheduleId}`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

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
| scheduleId | Long | 일정 ID | O |

**요청 예시**
```
DELETE /v1/admin/posts/12/schedules/5
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시글 매핑 일정 삭제 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[일정]이 성공적으로 삭제되었습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 일정 또는 게시글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [일정]입니다.",
  "data": null
}
```

---

### 비즈니스 로직
- 일정 삭제 시 연동된 게시글의 `hasSchedule`을 `false`로 업데이트
- 연동된 게시글의 `scheduleId`를 `null`로 업데이트
