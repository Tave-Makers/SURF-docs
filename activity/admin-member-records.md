## 특정 회원 활동기록 조회 (관리자)

### 개요
관리자가 특정 회원의 활동기록을 페이지네이션 방식으로 조회합니다.

### 엔드포인트
`GET /v1/admin/scores/members/{memberId}/activity-records`

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
| memberId | Long | 조회 대상 회원 ID | O |

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| pageNum | int | 페이지 번호 (0부터 시작) | O |
| pageSize | int | 페이지당 항목 수 | O |

**요청 예시**
```
GET /v1/admin/scores/members/1/activity-records?pageNum=0&pageSize=10
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array\<AdminActivityRecordResDTO\> | 활동 기록 목록 |
| content[].activityRecordId | String | 활동기록 ID (문자열로 직렬화) |
| content[].activityType | String | 활동 유형 enum 값 (예: `EARLY_BIRD`) |
| content[].activityName | String | 활동 유형 표시명 (예: "행사 얼리버드") |
| content[].scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) |
| content[].activityDate | String | 활동 날짜 (YYYY-MM-DD) |
| content[].appliedScore | BigDecimal | 적용된 점수 |
| pageNumber | int | 현재 페이지 번호 |
| pageSize | int | 페이지 크기 |
| numberOfElements | int | 현재 페이지의 실제 항목 수 |
| isLast | boolean | 마지막 페이지 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 기록]을 조회했습니다.",
  "data": {
    "content": [
      {
        "activityRecordId": "631799735897088000",
        "activityType": "EARLY_BIRD",
        "activityName": "행사 얼리버드",
        "scoreType": "REWARD",
        "activityDate": "2025-02-24",
        "appliedScore": 5.0
      },
      {
        "activityRecordId": "631799735897088001",
        "activityType": "SESSION_LATE_1_TO_10",
        "activityName": "정규 세션 지각",
        "scoreType": "PENALTY",
        "activityDate": "2025-02-17",
        "appliedScore": -10.0
      }
    ],
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 2,
    "isLast": true
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
| 403 Forbidden | 권한 부족 | 관리자 권한 필요 |
