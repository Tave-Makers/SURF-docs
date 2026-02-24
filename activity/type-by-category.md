## 특정 카테고리 활동 종류 조회

### 개요
특정 카테고리에 속한 활동 종류(ActivityType) 목록을 조회합니다.

### 엔드포인트
`GET /v1/manager/activity-type`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

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
| category | String | 카테고리 enum 값 (예: `REGULAR_SESSION`, `ACTIVITY` 등) | O |

**요청 예시**
```
GET /v1/manager/activity-type?category=REGULAR_SESSION
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
| category | Object | 카테고리 정보 |
| category.categoryName | String | 카테고리 enum 값 |
| category.categoryDisplayName | String | 카테고리 표시명 |
| activityTypeList | Array\<ActivityTypeDetailResDTO\> | 해당 카테고리의 활동 종류 목록 |
| activityTypeList[].typeName | String | 활동 유형 enum 값 |
| activityTypeList[].displayName | String | 활동 유형 표시명 |
| activityTypeList[].delta | Integer | 적용 점수 |
| activityTypeList[].scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) |
| activityTypeList[].appliedTarget | String | 적용 대상 (`INDIVIDUAL` 또는 `TEAM`) |
| activityTypeList[].category | String | 소속 카테고리 표시명 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[특정 활동 카테고리]를 조회합니다.",
  "data": {
    "category": {
      "categoryName": "REGULAR_SESSION",
      "categoryDisplayName": "정규 행사"
    },
    "activityTypeList": [
      {
        "typeName": "EARLY_BIRD",
        "displayName": "행사 얼리버드",
        "delta": 5,
        "scoreType": "REWARD",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_ABSENCE",
        "displayName": "정규 세션 결석",
        "delta": -30,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_TRUANCY",
        "displayName": "정규 세션 무단 결석",
        "delta": -100,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_LATE",
        "displayName": "정규 세션 지각",
        "delta": 0,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_LATE_1_TO_10",
        "displayName": "정규 세션 지각",
        "delta": -10,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_LATE_11_TO_20",
        "displayName": "정규 세션 지각",
        "delta": -20,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      },
      {
        "typeName": "SESSION_LATE_21_TO_30",
        "displayName": "정규 세션 지각",
        "delta": -30,
        "scoreType": "PENALTY",
        "appliedTarget": "INDIVIDUAL",
        "category": "정규 행사"
      }
    ]
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 요청 실패 | 유효하지 않은 카테고리 값 |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
