## 내 뱃지 조회

### 개요
마이페이지에서 본인의 활동 뱃지를 조회합니다 (무한스크롤).

### 엔드포인트
`GET /v1/user/members/badges`

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
| content | Array | 뱃지 목록 |
| content[].badgeName | String | 뱃지 이름 |
| content[].generation | Integer | 기수 |
| content[].awardedAt | String | 수여 일자 |
| pageNumber | Integer | 현재 페이지 번호 |
| pageSize | Integer | 페이지 크기 |
| numberOfElements | Integer | 현재 페이지 요소 수 |
| isLast | Boolean | 마지막 페이지 여부 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[활동 뱃지]가 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "badgeName": "우수회원 1위",
        "generation": 15,
        "awardedAt": "25.01.15"
      }
    ],
    "pageNumber": 0,
    "pageSize": 10,
    "numberOfElements": 1,
    "isLast": true
  }
}
```
