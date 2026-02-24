## 활동 카테고리 목록 조회

### 개요
활동 종류의 카테고리들만 조회합니다. 각 카테고리에 포함된 활동 종류(ActivityType)는 포함되지 않습니다.

### 엔드포인트
`GET /v1/manager/activity-categories`

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
| (root) | Array\<ActivityCategoryResDTO\> | 카테고리 목록 |
| [].categoryName | String | 카테고리 enum 값 |
| [].categoryDisplayName | String | 카테고리 표시명 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[모든 활동 카테고리]를 조회합니다.",
  "data": [
    {
      "categoryName": "STUDY_ON_PERSONAL",
      "categoryDisplayName": "스터디(개인)"
    },
    {
      "categoryName": "PROJECT_ON_PERSONAL",
      "categoryDisplayName": "프로젝트(개인)"
    },
    {
      "categoryName": "STUDY_ON_TEAM",
      "categoryDisplayName": "스터디(팀)"
    },
    {
      "categoryName": "PROJECT_ON_TEAM",
      "categoryDisplayName": "프로젝트(팀)"
    },
    {
      "categoryName": "REGULAR_SESSION",
      "categoryDisplayName": "정규 행사"
    },
    {
      "categoryName": "ACTIVITY",
      "categoryDisplayName": "활동"
    }
  ]
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
