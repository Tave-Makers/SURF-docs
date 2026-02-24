## 일정 수정

### 개요
일정을 수정합니다. 부분 수정을 지원하며, null이 아닌 필드만 업데이트됩니다.

### 엔드포인트
`PATCH /v1/admin/schedules/{scheduleId}`

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

**Body (ScheduleUpdateReqDTO)**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| category | String | 일정 카테고리 | X |
| title | String | 일정 제목 | X |
| startAt | String | 시작 시간 (ISO 8601) | X |
| endAt | String | 종료 시간 (ISO 8601) | X |
| location | String | 장소 | X |

**요청 예시**
```json
{
  "title": "수정된 만남의 장",
  "location": "세종대학교 대양홀"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 일정 수정 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[일정]이 성공적으로 수정되었습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 일정이 존재하지 않음 |
| 400 Bad Request | 잘못된 요청 | 시작 시간이 종료 시간 이후인 경우 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [일정]입니다.",
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
