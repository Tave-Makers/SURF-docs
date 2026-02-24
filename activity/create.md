## 활동기록 부여

### 개요
관리자가 회원에게 활동 점수(기록)를 부여합니다. 상점 또는 벌점을 부여할 수 있습니다.

### 엔드포인트
`POST /v1/admin/activity-records`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | Y |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| memberIdList | Array\<Long\> | 대상 회원 ID 목록 | Y |
| activityName | String | 활동 유형 (아래 ActivityType 참조) | Y |
| activityDate | String | 활동 날짜 (YYYY-MM-DD) | Y |

**ActivityType (상점)**
| 값 | 설명 | 점수 |
|----|------|------|
| ATTENDANCE | 출석 | +3 |
| STUDY_ATTENDANCE | 스터디 출석 | +3 |
| ASSIGNMENT_SUBMISSION | 과제 제출 | +5 |
| BLOG_SUBMISSION | 블로그 제출 | +5 |
| MENTORING_PARTICIPATION | 멘토링 참여 | +5 |
| EVENT_PARTICIPATION | 행사 참여 | +5 |
| EXCELLENT_STUDY | 우수 스터디 | +10 |
| ADVANCED_PROJECT | 심화 프로젝트 | +15 |
| COLLABORATIVE_PROJECT | 연합 프로젝트 | +15 |
| EXCELLENT_MEMBER | 우수 회원 | +20 |

**ActivityType (벌점)**
| 값 | 설명 | 점수 |
|----|------|------|
| ABSENCE | 결석 | -5 |
| LATE_SUBMISSION | 지각 제출 | -3 |
| UNEXCUSED_ABSENCE | 무단 결석 | -10 |

**요청 예시**
```json
{
  "memberIdList": [1, 2, 3],
  "activityName": "ATTENDANCE",
  "activityDate": "2025-02-24"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 부여 성공 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[활동 기록]이 성공적으로 부여되었습니다.",
  "data": null
}
```
