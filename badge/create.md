## 뱃지 부여

### 개요
관리자가 회원에게 활동 뱃지를 부여합니다.

### 엔드포인트
`POST /v1/admin/members/badges`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `ADMIN`, `PRESIDENT`, `MANAGER`

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
| badgeType | String | 뱃지 타입 (아래 BadgeType 참조) | Y |
| memberIdList | Array\<Long\> | 뱃지를 부여할 회원 ID 목록 | Y |

**BadgeType**
| 값 | 설명 |
|----|------|
| EXCELLENT_MEMBER_1ST | 우수회원 1위 |
| EXCELLENT_MEMBER_2ND | 우수회원 2위 |
| EXCELLENT_MEMBER_3RD | 우수회원 3위 |
| EXCELLENT_STUDY_1ST | 우수 스터디 |
| ADVANCED_PROJECT_1ST | 심화 프로젝트 1위 |
| ADVANCED_PROJECT_2ND | 심화 프로젝트 2위 |
| COLLABORATIVE_PROJECT_1ST | 연합 프로젝트 1위 |
| COLLABORATIVE_PROJECT_2ND | 연합 프로젝트 2위 |

**요청 예시**
```json
{
  "badgeType": "EXCELLENT_MEMBER_1ST",
  "memberIdList": [1, 2, 3]
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
  "message": "[활동 뱃지]가 성공적으로 부여되었습니다.",
  "data": null
}
```
