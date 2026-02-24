## 피드백 조회

### 개요
운영진이 피드백을 조회합니다.

### 엔드포인트
`GET /v1/admin/feedbacks`

### 인증
- **인증 필요 여부:** JWT 인증 필요 (PreAuthorize)
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

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
| page | Integer | 페이지 번호 (기본값: 0) | N |
| size | Integer | 페이지 크기 (기본값: 20) | N |
| sort | String | 정렬 (기본값: createdAt,desc) | N |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| content | Array | 피드백 목록 (Slice) |
| content[].id | Long | 피드백 ID |
| content[].content | String | 피드백 내용 |
| content[].createdAt | String | 생성 시간 |
| last | Boolean | 마지막 페이지 여부 |
| numberOfElements | Integer | 현재 페이지 요소 수 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[피드백]이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
        "id": 3,
        "content": "기능을 개선해주세요",
        "createdAt": "2025-10-05T14:50:00"
      },
      {
        "id": 2,
        "content": "버그가 있습니다",
        "createdAt": "2025-10-05T14:49:00"
      }
    ],
    "last": true,
    "numberOfElements": 2
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 403 Forbidden | 권한 부족 | 운영진 권한이 없음 |

**응답 예시**
```json
{
  "code": 403,
  "message": "권한이 부족합니다.",
  "data": null
}
```
