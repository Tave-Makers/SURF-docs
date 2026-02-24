## 활동점수 조회 (고정 5개 포함)

### 개요
개인 활동점수와 최근 고정된 5개의 활동기록을 함께 조회합니다.

### 엔드포인트
`GET /v1/user/members/personal-score/pinned5`

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

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| personalScore | BigDecimal | 개인 활동점수 |
| pinnedRecords | Array\<ActivityRecordResDTO\> | 고정된 최근 5개 활동기록 |
| pinnedRecords[].memberId | Long | 회원 ID |
| pinnedRecords[].categoryName | String | 활동 카테고리명 |
| pinnedRecords[].activityName | String | 활동 유형명 |
| pinnedRecords[].scoreType | String | 점수 유형 (`REWARD` 또는 `PENALTY`) |
| pinnedRecords[].appliedScore | BigDecimal | 적용된 점수 |
| pinnedRecords[].prefixSum | BigDecimal | 누적 점수 |
| pinnedRecords[].activityDate | String | 활동 날짜 (YY.MM.DD 형식) |

> 기본 점수: YB(신입) = 100점, 기존 회원 = 50점

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 점수]가 성공적으로 조회되었습니다.",
  "data": {
    "personalScore": 105.0,
    "pinnedRecords": [
      {
        "memberId": 1,
        "categoryName": "정규 행사",
        "activityName": "행사 얼리버드",
        "scoreType": "REWARD",
        "appliedScore": 5.0,
        "prefixSum": 105.0,
        "activityDate": "25.02.24"
      }
    ]
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 조회 실패 | 개인활동점수를 조회할 수 없음 |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |

**응답 예시**
```json
{
  "code": 400,
  "message": "[개인활동점수]를 조회할 수 없습니다.",
  "data": null
}
```
