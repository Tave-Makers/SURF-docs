## 특정 팀 멤버별 점수 현황 조회

### 개요
특정 팀에 속한 멤버들의 개인별 상/벌점 현황을 totalScore 내림차순으로 조회합니다.
팀 정보(teamId, teamName)와 함께 소속 멤버 목록이 반환됩니다.

### 엔드포인트
`GET /v1/admin/scores/teams/{teamId}/members`

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

**Path Variables**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| teamId | Long | 조회할 팀 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| teamId | Long | 팀 ID |
| teamName | String | 팀 이름 |
| members | Array | 멤버별 점수 목록 |
| members[].memberId | Long | 멤버 ID |
| members[].profileImageUrl | String | 프로필 이미지 URL |
| members[].name | String | 멤버 이름 |
| members[].part | String | 파트명 (최신 기수 기준, 없으면 null) |
| members[].rewardTotal | BigDecimal | 상점 누적 합계 |
| members[].penaltyTotal | BigDecimal | 벌점 누적 합계 (양수로 표시) |
| members[].totalScore | BigDecimal | 총 활동점수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[팀 멤버 점수 현황]을 조회했습니다.",
  "data": {
    "teamId": 1,
    "teamName": "SURF 프로젝트팀",
    "members": [
      {
        "memberId": 1,
        "profileImageUrl": "https://example.com/profile/1.jpg",
        "name": "홍길동",
        "part": "WEB",
        "rewardTotal": 25.0,
        "penaltyTotal": 10.0,
        "totalScore": 115.0
      },
      {
        "memberId": 3,
        "profileImageUrl": "https://example.com/profile/3.jpg",
        "name": "이영희",
        "part": "DESIGN",
        "rewardTotal": 10.0,
        "penaltyTotal": 0.0,
        "totalScore": 110.0
      }
    ]
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 없음 | MANAGER 이상 권한 필요 |
| 404 Not Found | 팀 없음 | 해당 teamId의 팀이 존재하지 않음 |
