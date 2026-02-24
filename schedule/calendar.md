## 월별 일정 조회

### 개요
캘린더 페이지에서 월별 일정을 조회합니다. MEMBER 권한은 "정규행사", "기타일정" 카테고리만 조회 가능하며, ADMIN 이상은 모든 카테고리를 조회할 수 있습니다.

### 엔드포인트
`GET /v1/user/calendar/schedules`

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

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| year | int | 조회 연도 | O |
| month | int | 조회 월 | O |

**요청 예시**
```
GET /v1/user/calendar/schedules?year=2025&month=11
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 월별 일정 조회 성공 |

**Body (ScheduleMonthlyResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| year | Integer | 조회 연도 |
| month | Integer | 조회 월 |
| scheduleResDTOList | Array | 일정 목록 |
| scheduleResDTOList[].scheduleId | Long | 일정 ID |
| scheduleResDTOList[].category | String | 일정 카테고리 |
| scheduleResDTOList[].title | String | 일정 제목 |
| scheduleResDTOList[].startAt | String | 시작 시간 (ISO 8601) |
| scheduleResDTOList[].endAt | String | 종료 시간 (ISO 8601) |
| scheduleResDTOList[].location | String | 장소 |
| scheduleResDTOList[].mappedByPost | Boolean | 게시글 연동 여부 |
| scheduleResDTOList[].postId | Long | 연동 게시글 ID (없으면 null) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[일정]이 성공적으로 월별 조회되었습니다.",
  "data": {
    "year": 2025,
    "month": 11,
    "scheduleResDTOList": [
      {
        "scheduleId": 5,
        "category": "정규행사",
        "title": "만남의 장",
        "startAt": "2025-11-15T14:00:00",
        "endAt": "2025-11-15T16:00:00",
        "location": "세종대학교 광개토대왕관",
        "mappedByPost": true,
        "postId": 12
      },
      {
        "scheduleId": 8,
        "category": "기타일정",
        "title": "OT",
        "startAt": "2025-11-20T10:00:00",
        "endAt": "2025-11-20T12:00:00",
        "location": "온라인",
        "mappedByPost": false,
        "postId": null
      }
    ]
  }
}
```

---

### 비즈니스 로직
- MEMBER 권한: "정규행사", "기타일정" 카테고리만 조회 가능
- ADMIN 이상 권한: 모든 카테고리 조회 가능

---

---

## 일정 단건 조회 (관리자)

### 개요
특정 일정을 조회합니다. 캘린더에서 일정을 수정/삭제할 때 사용합니다.

### 엔드포인트
`GET /v1/admin/calendar/schedules/{scheduleId}`

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
| scheduleId | Long | 일정 ID | O |

**요청 예시**
```
GET /v1/admin/calendar/schedules/5
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 일정 조회 성공 |

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
  "message": "[일정]이 성공적으로 조회되었습니다.",
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
| 404 Not Found | 리소스 없음 | 일정이 존재하지 않음 |

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

## 개별 일정 생성 (캘린더)

### 개요
캘린더에서 개별 일정을 생성합니다.

### 엔드포인트
`POST /v1/admin/calendar/schedules`

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
| 201 Created | 일정 생성 성공 |

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
| 400 Bad Request | 잘못된 요청 | 시작 시간이 종료 시간 이후인 경우 |

**응답 예시**
```json
{
  "code": 400,
  "message": "시작 시간이 종료 시간보다 이후일 수 없습니다.",
  "data": null
}
```
