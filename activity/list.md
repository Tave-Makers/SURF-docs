## 활동기록 조회 (무한스크롤)

### 개요
본인의 활동 기록을 페이지네이션(무한스크롤) 방식으로 조회합니다. 상점(REWARD) 또는 벌점(PENALTY) 기준으로 필터링하여 조회할 수 있습니다.

### 엔드포인트
`GET /v1/user/members/activity-records`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

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
| scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) | O |
| pageSize | int | 페이지당 항목 수 | O |
| pageNum | int | 페이지 번호 (0부터 시작) | O |

**요청 예시**
```
GET /v1/user/members/activity-records?scoreType=REWARD&pageSize=10&pageNum=0
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
| content | Array\<ActivityRecordResDTO\> | 활동 기록 목록 |
| content[].memberId | Long | 회원 ID |
| content[].categoryName | String | 활동 카테고리명 (대주제가 없을 경우 활동유형 표시명) |
| content[].activityName | String | 활동 유형명 (대주제가 없을 경우 null) |
| content[].scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) |
| content[].activityDate | String | 활동 날짜 (YY.MM.DD 형식) |
| content[].prefixSum | BigDecimal | 누적 점수 |
| content[].appliedScore | BigDecimal | 해당 활동으로 적용된 점수 |
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
        "memberId": 1,
        "categoryName": "정규 행사",
        "activityName": "행사 얼리버드",
        "scoreType": "REWARD",
        "activityDate": "25.02.24",
        "prefixSum": 105.0,
        "appliedScore": 5.0
      },
      {
        "memberId": 1,
        "categoryName": "활동",
        "activityName": "뒷풀이 참여",
        "scoreType": "REWARD",
        "activityDate": "25.02.17",
        "prefixSum": 100.0,
        "appliedScore": 5.0
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
| 400 Bad Request | 요청 실패 | 유효하지 않은 요청 파라미터 (scoreType 등) |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
