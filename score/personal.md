## 활동점수 + 고정 5개 활동기록 조회

### 개요
로그인한 사용자의 개인 활동점수와 고정된 활동기록 요약(상점/벌점 그룹별 횟수)을 조회합니다.
상점은 TAVE 활동(인스타그램 스토리 업로드, 기술 세미나 참여, 얼리버드)과 블로그(WIL 작성, TAVE 활동 후기 업로드) 그룹으로 나뉘며,
벌점은 지각(정규 세션 지각, 팀 지각)과 결석(정규 세션 결석, 팀 결석) 그룹으로 나뉩니다.

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

별도의 Query Parameter, Path Variable, Request Body 없음. JWT 토큰에서 현재 로그인 사용자 ID를 추출합니다.

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| score | BigDecimal | 개인 활동점수 (기본값: YB=100, 기존회원=50) |
| records | Object | 고정 활동기록 요약 |
| records.rewards | Object | 상점 그룹 |
| records.rewards.taveActivities | Array | TAVE 활동 상점 목록 |
| records.rewards.taveActivities[].activityType | String | 활동 유형 enum name (예: UPLOAD_INSTAGRAM_STORY) |
| records.rewards.taveActivities[].count | Long | 해당 활동 횟수 |
| records.rewards.blogs | Object | 블로그 상점 그룹 |
| records.rewards.blogs.totalCount | int | 블로그 상점 총 횟수 |
| records.rewards.blogs.list | Array | 블로그 상점 상세 목록 |
| records.rewards.blogs.list[].activityType | String | 활동 유형 enum name (예: WRITE_WIL) |
| records.rewards.blogs.list[].count | Long | 해당 활동 횟수 |
| records.penalties | Object | 벌점 그룹 |
| records.penalties.late | Object | 지각 벌점 그룹 |
| records.penalties.late.totalCount | int | 지각 총 횟수 |
| records.penalties.late.list | Array | 지각 상세 목록 |
| records.penalties.late.list[].activityType | String | 활동 유형 enum name (예: SESSION_LATE) |
| records.penalties.late.list[].count | Long | 해당 유형 합산 횟수 |
| records.penalties.absence | Object | 결석 벌점 그룹 |
| records.penalties.absence.totalCount | int | 결석 총 횟수 |
| records.penalties.absence.list | Array | 결석 상세 목록 |
| records.penalties.absence.list[].activityType | String | 활동 유형 enum name (예: SESSION_ABSENCE) |
| records.penalties.absence.list[].count | Long | 해당 유형 합산 횟수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[개인활동점수]와 [고정활동내역]을 조회합니다.",
  "data": {
    "score": 103.0,
    "records": {
      "rewards": {
        "taveActivities": [
          {
            "activityType": "UPLOAD_INSTAGRAM_STORY",
            "count": 1
          },
          {
            "activityType": "ENGAGE_TECH_SEMINAR",
            "count": 0
          },
          {
            "activityType": "EARLY_BIRD",
            "count": 1
          }
        ],
        "blogs": {
          "totalCount": 1,
          "list": [
            {
              "activityType": "WRITE_WIL",
              "count": 1
            },
            {
              "activityType": "UPLOAD_TAVE_REVIEW",
              "count": 0
            }
          ]
        }
      },
      "penalties": {
        "late": {
          "totalCount": 1,
          "list": [
            {
              "activityType": "SESSION_LATE",
              "count": 1
            },
            {
              "activityType": "TEAM_LATE",
              "count": 0
            }
          ]
        },
        "absence": {
          "totalCount": 0,
          "list": [
            {
              "activityType": "SESSION_ABSENCE",
              "count": 0
            },
            {
              "activityType": "TEAM_ABSENCE",
              "count": 0
            }
          ]
        }
      }
    }
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 조회 실패 | 개인활동점수를 조회할 수 없음 |

**응답 예시**
```json
{
  "code": 400,
  "message": "[개인활동점수]를 조회할 수 없습니다.",
  "data": null
}
```
