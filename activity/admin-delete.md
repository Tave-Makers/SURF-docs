## 활동기록 삭제 (관리자)

### 개요
관리자가 특정 활동기록을 삭제(소프트 삭제)합니다. 이미 삭제된 기록을 다시 삭제하려 하면 에러가 발생합니다.

### 엔드포인트
`DELETE /v1/admin/activity-records/{activityRecordId}`

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
| activityRecordId | Long | 삭제 대상 활동기록 ID | O |

**요청 예시**
```
DELETE /v1/admin/activity-records/631799735897088000
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 삭제 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 기록]을 삭제했습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 요청 실패 | 이미 삭제된 활동기록 |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
| 403 Forbidden | 권한 부족 | 관리자 권한 필요 |
| 404 Not Found | 조회 실패 | 해당 활동기록을 찾을 수 없음 |
