## 1. 개인별 상/벌점 현황 조회

### 개요
활동 멤버들의 개인별 상/벌점 현황을 totalScore 내림차순으로 조회합니다.
탈퇴(WITHDRAWN) 상태의 멤버는 제외되며, 무한스크롤(Slice) 형태의 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/admin/scores/members`

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

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| pageNum | int | 페이지 번호 (0부터 시작) | O |
| pageSize | int | 한 페이지당 항목 수 | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array | 멤버별 점수 목록 |
| content[].memberId | Long | 멤버 ID |
| content[].profileImageUrl | String | 프로필 이미지 URL |
| content[].name | String | 멤버 이름 |
| content[].part | String | 파트명 (최신 기수 기준, 없으면 null) |
| content[].rewardTotal | BigDecimal | 상점 누적 합계 |
| content[].penaltyTotal | BigDecimal | 벌점 누적 합계 (양수로 표시) |
| content[].totalScore | BigDecimal | 총 활동점수 |
| pageNumber | int | 현재 페이지 번호 |
| pageSize | int | 페이지 크기 |
| numberOfElements | int | 현재 페이지의 항목 수 |
| isLast | boolean | 마지막 페이지 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[개인별 상/벌점 현황]을 조회합니다.",
  "data": {
    "content": [
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
        "memberId": 2,
        "profileImageUrl": "https://example.com/profile/2.jpg",
        "name": "김철수",
        "part": "SERVER",
        "rewardTotal": 15.0,
        "penaltyTotal": 30.0,
        "totalScore": 85.0
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
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 없음 | MANAGER 이상 권한 필요 |

---
---

## 2. 팀별 상/벌점 현황 조회

### 개요
팀별 상/벌점 현황을 totalScore 내림차순으로 조회합니다.
선택적으로 generation 파라미터를 전달하여 특정 기수의 팀만 필터링할 수 있으며, 무한스크롤(Slice) 형태의 페이지네이션을 지원합니다.

### 엔드포인트
`GET /v1/admin/scores/teams`

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

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| generation | Integer | 기수 필터 (미전달 시 전체 조회) | X |
| pageNum | int | 페이지 번호 (0부터 시작) | O |
| pageSize | int | 한 페이지당 항목 수 | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array | 팀별 점수 목록 |
| content[].teamId | Long | 팀 ID |
| content[].teamName | String | 팀 이름 |
| content[].teamType | String | 팀 유형 (STUDY / PROJECT) |
| content[].rewardTotal | BigDecimal | 상점 누적 합계 |
| content[].penaltyTotal | BigDecimal | 벌점 누적 합계 (양수로 표시) |
| content[].totalScore | BigDecimal | 총 활동점수 |
| pageNumber | int | 현재 페이지 번호 |
| pageSize | int | 페이지 크기 |
| numberOfElements | int | 현재 페이지의 항목 수 |
| isLast | boolean | 마지막 페이지 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[팀별 상/벌점 현황]을 조회합니다.",
  "data": {
    "content": [
      {
        "teamId": 1,
        "teamName": "SURF 프로젝트팀",
        "teamType": "PROJECT",
        "rewardTotal": 0.0,
        "penaltyTotal": 5.0,
        "totalScore": -5.0
      },
      {
        "teamId": 2,
        "teamName": "Spring 스터디",
        "teamType": "STUDY",
        "rewardTotal": 0.0,
        "penaltyTotal": 10.0,
        "totalScore": -10.0
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
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 없음 | MANAGER 이상 권한 필요 |

---
---

## 3. 특정 팀 멤버별 점수 현황 조회

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
