## 활동 종류 전체 조회

### 개요
모든 활동 카테고리와 각 카테고리에 포함된 활동 종류(ActivityType)를 함께 조회합니다.

### 엔드포인트
`GET /v1/manager/activity-types`

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

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| (root) | Array\<ActivityCategoryDetailResDTO\> | 카테고리별 활동 종류 목록 |
| [].category | Object | 카테고리 정보 |
| [].category.categoryName | String | 카테고리 enum 값 (예: `REGULAR_SESSION`) |
| [].category.categoryDisplayName | String | 카테고리 표시명 (예: "정규 행사") |
| [].activityTypeList | Array\<ActivityTypeDetailResDTO\> | 해당 카테고리의 활동 종류 목록 |
| [].activityTypeList[].typeName | String | 활동 유형 enum 값 (예: `EARLY_BIRD`) |
| [].activityTypeList[].displayName | String | 활동 유형 표시명 (예: "행사 얼리버드") |
| [].activityTypeList[].delta | Integer | 적용 점수 (양수: 상점, 음수: 벌점) |
| [].activityTypeList[].scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) |
| [].activityTypeList[].appliedTarget | String | 적용 대상 (`INDIVIDUAL` 또는 `TEAM`) |
| [].activityTypeList[].category | String | 소속 카테고리 표시명 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[모든 활동 종류]를 조회합니다.",
  "data": [
    {
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
        }
      ]
    },
    {
      "category": {
        "categoryName": "ACTIVITY",
        "categoryDisplayName": "활동"
      },
      "activityTypeList": [
        {
          "typeName": "ENGAGE_AFTER_PARTY",
          "displayName": "뒷풀이 참여",
          "delta": 5,
          "scoreType": "REWARD",
          "appliedTarget": "INDIVIDUAL",
          "category": "활동"
        }
      ]
    }
  ]
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
