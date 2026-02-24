## 알림 읽음 처리

### 개요
특정 알림을 읽음 처리합니다.

### 엔드포인트
`PATCH /v1/user/notifications/{notificationId}/read`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| notificationId | Long | 알림 ID | Y |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 읽음 처리 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[알람]이 성공적으로 읽음 처리되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 알림 없음 | 해당 알림을 찾을 수 없음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "요청하신 [알람]을 찾을 수 없습니다.",
  "data": null
}
```
