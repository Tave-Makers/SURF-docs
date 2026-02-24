## 멘션 검색

### 개요
이름을 기반으로 멘션 가능한 회원을 검색합니다. 최대 10명이 반환되며, 최신 기수 순으로 정렬됩니다.

### 엔드포인트
`GET /v1/user/comments/mentions/search`

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
| keyword | String | 검색 키워드 (최소 2글자 이상) | O |

**요청 예시**
```
GET /v1/user/comments/mentions/search?keyword=홍길
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 검색 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| memberId | Long | 회원 ID |
| nickname | String | 닉네임 |
| profileImageUrl | String | 프로필 이미지 URL |
| firstGeneration | Integer | 최초 기수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[멘션 검색]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "memberId": 2,
      "nickname": "홍길동",
      "profileImageUrl": "https://example.com/profile.jpg",
      "firstGeneration": 13
    },
    {
      "memberId": 12,
      "nickname": "홍창준",
      "profileImageUrl": "https://example.com/profile2.jpg",
      "firstGeneration": 15
    }
  ]
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효성 검증 실패 | 검색어가 2글자 미만 |

**응답 예시**
```json
{
  "code": 400,
  "message": "회원 멘션 시 이름은 두 글자 이상 입력해주세요.",
  "data": null
}
```
