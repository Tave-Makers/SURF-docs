## 피드백 생성

### 개요
익명 피드백을 생성합니다. 하루 최대 3회까지 작성할 수 있습니다.

### 엔드포인트
`POST /v1/user/feedbacks`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

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
| content | String | 피드백 내용 (최대 500자) | Y |

**요청 예시**
```json
{
  "content": "더 많은 네트워킹 시간이 있었으면 좋겠습니다."
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 생성 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| id | Long | 피드백 ID |
| content | String | 피드백 내용 |
| createdAt | String | 생성 시간 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[피드백]이 성공적으로 생성되었습니다.",
  "data": {
    "id": 1,
    "content": "더 많은 네트워킹 시간이 있었으면 좋겠습니다.",
    "createdAt": "2025-02-24T14:48:00"
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 429 Too Many Requests | 한도 초과 | 하루 3회 작성 제한 초과 |

**응답 예시**
```json
{
  "code": 429,
  "message": "하루에 3개의 [피드백]만 작성할 수 있습니다.",
  "data": null
}
```
