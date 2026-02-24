## 팀별 상/벌점 현황 조회

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
