## 활동기록 수정 (관리자)

### 개요
관리자가 특정 활동기록의 활동 유형(activityType)과 활동 날짜(activityDate)를 수정합니다. 활동 유형이 변경되면 점수 차이가 자동으로 반영됩니다.

### 엔드포인트
`PATCH /v1/admin/activity-records/{activityRecordId}`

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
| activityRecordId | Long | 수정 대상 활동기록 ID | O |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| activityType | String | 변경할 활동 유형 (ActivityType enum) | X |
| activityDate | String | 변경할 활동 날짜 (YYYY-MM-DD) | X |

> 두 필드 모두 선택적(optional)입니다. 전달된 필드만 업데이트됩니다.

**요청 예시**
```json
{
  "activityType": "SESSION_LATE_11_TO_20",
  "activityDate": "2025-02-25"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 수정 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 기록]을 수정했습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 요청 실패 | 유효하지 않은 요청 파라미터 |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
| 403 Forbidden | 권한 부족 | 관리자 권한 필요 |
| 404 Not Found | 조회 실패 | 해당 활동기록을 찾을 수 없음 |
