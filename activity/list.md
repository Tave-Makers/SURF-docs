## 활동기록 조회

### 개요
본인의 활동 기록을 무한스크롤 방식으로 조회합니다.

### 엔드포인트
`GET /v1/user/members/activity-records`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | Y |

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| pageNum | Integer | 페이지 번호 (기본값: 0) | N |
| pageSize | Integer | 페이지 크기 | N |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array | 활동 기록 목록 |
| content[].categoryName | String | 활동 카테고리명 |
| content[].activityName | String | 활동 유형명 |
| content[].scoreType | String | REWARD(상점) / PENALTY(벌점) |
| content[].appliedScore | BigDecimal | 적용된 점수 |
| content[].prefixSum | BigDecimal | 누적 점수 |
| content[].activityDate | String | 활동 날짜 (YY.MM.DD) |
| pageNumber | Integer | 현재 페이지 번호 |
| pageSize | Integer | 페이지 크기 |
| numberOfElements | Integer | 현재 페이지 요소 수 |
| isLast | Boolean | 마지막 페이지 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 기록]이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "categoryName": "출석",
        "activityName": "정규 세션 출석",
        "scoreType": "REWARD",
        "appliedScore": 3.0,
        "prefixSum": 103.0,
        "activityDate": "25.02.24"
      }
    ],
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 1,
    "isLast": true
  }
}
```
