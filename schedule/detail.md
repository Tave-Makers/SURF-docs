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
