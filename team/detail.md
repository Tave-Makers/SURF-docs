## 팀 상세 조회

### 개요
특정 팀의 상세 정보를 조회합니다. 팀 기본 정보, 팀장 정보, 팀원 목록(프로필 이미지, 트랙 포함)을 반환합니다.

### 엔드포인트
`GET /v1/admin/teams/{teamId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| teamId | Long | 조회할 팀의 ID | O |

**요청 예시**
```
GET /v1/admin/teams/1
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
| data | Object | 팀 상세 정보 |
| data.teamId | Long | 팀 ID |
| data.generation | Integer | 기수 |
| data.type | String | 팀 유형 (`STUDY`, `PROJECT`) |
| data.name | String | 팀명 |
| data.description | String | 팀 소개 |
| data.leader | Object | 팀장 정보 |
| data.leader.memberId | Long | 팀장 Member ID |
| data.leader.name | String | 팀장 이름 |
| data.leader.profileImageUrl | String | 팀장 프로필 이미지 URL |
| data.leader.tracks | Array | 팀장 트랙 목록 |
| data.leader.tracks[].generation | Integer | 트랙 기수 |
| data.leader.tracks[].part | String | 파트 이름 (예: `BACKEND`) |
| data.members | Array | 팀원 목록 |
| data.members[].memberId | Long | 팀원 Member ID |
| data.members[].name | String | 팀원 이름 |
| data.members[].profileImageUrl | String | 팀원 프로필 이미지 URL |
| data.members[].tracks | Array | 팀원 트랙 목록 |
| data.members[].tracks[].generation | Integer | 트랙 기수 |
| data.members[].tracks[].part | String | 파트 이름 (예: `BACKEND`) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[팀]이 성공적으로 조회되었습니다.",
  "data": {
    "teamId": 1,
    "generation": 15,
    "type": "STUDY",
    "name": "Spring 스터디",
    "description": "Spring Boot 심화 학습을 위한 스터디입니다.",
    "leader": {
      "memberId": 1,
      "name": "홍길동",
      "profileImageUrl": "https://example.com/images/profile1.jpg",
      "tracks": [
        {
          "generation": 15,
          "part": "BACKEND"
        }
      ]
    },
    "members": [
      {
        "memberId": 1,
        "name": "홍길동",
        "profileImageUrl": "https://example.com/images/profile1.jpg",
        "tracks": [
          {
            "generation": 15,
            "part": "BACKEND"
          }
        ]
      },
      {
        "memberId": 2,
        "name": "김철수",
        "profileImageUrl": "https://example.com/images/profile2.jpg",
        "tracks": [
          {
            "generation": 15,
            "part": "FRONTEND"
          }
        ]
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
| 403 Forbidden | 권한 부족 | 관리자 권한이 없음 |
| 404 Not Found | 팀 없음 | 존재하지 않는 [팀]입니다. |
