## 쪽지 전송

### 개요
다른 회원에게 쪽지를 전송합니다. 수신자에게 이메일과 푸시 알림이 발송됩니다.

### 엔드포인트
`POST /v1/user/letters`

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

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| receiverId | Long | 수신자 회원 ID | O |
| title | String | 쪽지 제목 (최대 100자) | O |
| content | String | 쪽지 본문 (최대 10000자) | O |
| sns | String | 추가 연락 SNS (최대 100자) | X |
| replyEmail | String | 회신 받을 이메일 (최대 100자, 이메일 형식) | O |

**요청 예시**
```json
{
  "receiverId": 3,
  "title": "문의드립니다.",
  "content": "안녕하세요, 몇 가지 질문이 있습니다.",
  "sns": "@instagram_user",
  "replyEmail": "sender@example.com"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 전송 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| letterId | Long | 쪽지 ID |
| title | String | 쪽지 제목 |
| content | String | 쪽지 본문 |
| sns | String | 추가 연락 SNS |
| replyEmail | String | 회신 이메일 |
| senderId | Long | 발신자 회원 ID |
| senderName | String | 발신자 이름 |
| receiverId | Long | 수신자 회원 ID |
| receiverName | String | 수신자 이름 |
| createdAt | String | 전송일시 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[쪽지]가 성공적으로 전송되었습니다.",
  "data": {
    "letterId": 12,
    "title": "문의드립니다.",
    "content": "안녕하세요, 몇 가지 질문이 있습니다.",
    "sns": "@instagram_user",
    "replyEmail": "sender@example.com",
    "senderId": 1,
    "senderName": "홍길동",
    "receiverId": 3,
    "receiverName": "김영희",
    "createdAt": "2025-12-25T14:12:33"
  }
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효성 검증 실패 | 필수 필드 누락, 형식 오류 등 |
| 404 Not Found | 리소스 없음 | 수신자가 존재하지 않음 |
| 500 Internal Server Error | 서버 오류 | 이메일 발송 실패 |

**응답 예시**
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```

```json
{
  "code": 404,
  "message": "존재하지 않는 [회원]입니다.",
  "data": null
}
```

```json
{
  "code": 500,
  "message": "메일 발송에 실패했습니다.",
  "data": null
}
```
