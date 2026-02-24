## 보낸 쪽지 목록

### 개요
자신이 보낸 쪽지 목록을 최신순으로 조회합니다.

### 엔드포인트
`GET /v1/user/letters/sent`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Query Parameters**
| Key | Type | 설명 | 필수 | 기본값 |
|-----|------|------|------|--------|
| page | Integer | 페이지 번호 | X | 0 |
| size | Integer | 페이지 크기 | X | 10 |

**요청 예시**
```
GET /v1/user/letters/sent?page=0&size=10
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body (Slice\<LetterResDTO\>)**
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
  "message": "[쪽지] 보낸 목록이 성공적으로 조회되었습니다.",
  "data": {
    "content": [
      {
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
    ],
    "last": true,
    "numberOfElements": 1
  }
}
```
