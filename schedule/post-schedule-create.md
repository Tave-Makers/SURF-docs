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
