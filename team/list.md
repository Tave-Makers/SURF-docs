## 팀 목록 조회

### 개요
팀 목록을 기수별로 그룹핑하여 조회합니다. `type` 파라미터를 통해 스터디/프로젝트를 필터링할 수 있으며, 파라미터를 생략하면 전체 팀을 조회합니다.

### 엔드포인트
`GET /v1/admin/teams`

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
| Key | Type | 설명 | 필수 | 비고 |
|-----|------|------|------|------|
| type | String | 팀 유형 필터 (`STUDY`, `PROJECT`) | X | 미입력 시 전체 조회 |

**요청 예시**
```
GET /v1/admin/teams
GET /v1/admin/teams?type=STUDY
GET /v1/admin/teams?type=PROJECT
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
| code | Integer | HTTP 상태 코드 |
| message | String | 응답 메시지 |
| data | Array | 기수별 팀 목록 |
| data[].generation | Integer | 기수 |
| data[].teams | Array | 해당 기수의 팀 리스트 |
| data[].teams[].teamId | Long | 팀 ID |
| data[].teams[].generation | Integer | 기수 |
| data[].teams[].type | String | 팀 유형 (`STUDY`, `PROJECT`) |
| data[].teams[].name | String | 팀명 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[팀]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "generation": 15,
      "teams": [
        {
          "teamId": 1,
          "generation": 15,
          "type": "STUDY",
          "name": "Spring 스터디"
        },
        {
          "teamId": 2,
          "generation": 15,
          "type": "PROJECT",
          "name": "SURF 프로젝트"
        }
      ]
    },
    {
      "generation": 14,
      "teams": [
        {
          "teamId": 3,
          "generation": 14,
          "type": "STUDY",
          "name": "알고리즘 스터디"
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
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 부족 | 관리자 권한이 없음 |
