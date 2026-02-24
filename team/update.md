## 팀 수정

### 개요
기존 팀 정보를 새로운 정보로 완전히 대체(PUT)합니다. 팀장의 `leaderMemberId`는 반드시 팀원 목록 `memberIds`에 포함되어야 합니다.

### 엔드포인트
`PUT /v1/admin/teams/{teamId}`

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
| Content-Type | String | `application/json` | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| teamId | Long | 수정할 팀의 ID | O |

**Body**
| Key | Type | 설명 | 필수 | 제약 조건 |
|-----|------|------|------|-----------|
| generation | Integer | 기수 | O | |
| type | String | 팀 유형 (`STUDY`, `PROJECT`) | O | |
| name | String | 팀명 | O | 최대 50자 |
| description | String | 팀 소개 | O | 최대 500자 |
| leaderMemberId | Long | 팀장의 Member ID | O | `memberIds`에 포함되어야 함 |
| memberIds | Long[] | 팀원 Member ID 리스트 | O | 1명 이상, 중복 불가 |

**요청 예시**
```json
PUT /v1/admin/teams/1

{
  "generation": 15,
  "type": "STUDY",
  "name": "Spring 심화 스터디",
  "description": "Spring Boot 심화 학습 및 프로젝트 적용을 위한 스터디입니다.",
  "leaderMemberId": 2,
  "memberIds": [1, 2, 3, 5]
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 팀 수정 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| code | Integer | HTTP 상태 코드 |
| message | String | 응답 메시지 |
| data | Object | 수정된 팀 정보 |
| data.teamId | Long | 팀 ID |
| data.generation | Integer | 기수 |
| data.type | String | 팀 유형 (`STUDY`, `PROJECT`) |
| data.name | String | 팀명 |
| data.description | String | 팀 소개 |
| data.leaderId | Long | 팀장 Member ID |
| data.leaderName | String | 팀장 이름 |
| data.memberCount | Integer | 팀원 수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[팀]이 성공적으로 수정되었습니다.",
  "data": {
    "teamId": 1,
    "generation": 15,
    "type": "STUDY",
    "name": "Spring 심화 스터디",
    "description": "Spring Boot 심화 학습 및 프로젝트 적용을 위한 스터디입니다.",
    "leaderId": 2,
    "leaderName": "김철수",
    "memberCount": 4
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 잘못된 요청 | 필수 필드 누락, 유효성 검증 실패 |
| 400 Bad Request | 중복 팀원 | 리스트 내에 중복된 [팀원]ID가 존재합니다. |
| 400 Bad Request | 팀장 미포함 | 팀에 존재하지 않는 [팀장]입니다. |
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 부족 | 관리자 권한이 없음 |
| 404 Not Found | 팀 없음 | 존재하지 않는 [팀]입니다. |
| 404 Not Found | 팀장 없음 | 존재하지 않는 [팀장]입니다. |
