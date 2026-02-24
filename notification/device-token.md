## FCM 토큰 등록

### 개요
디바이스의 FCM 토큰을 서버에 등록합니다. 푸시 알림 수신을 위해 앱 실행 시 또는 토큰 갱신 시 호출해야 합니다.

### 엔드포인트
`POST /v1/user/notifications/device-tokens`

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

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| token | String | FCM 디바이스 토큰 | Y |
| platform | String | 플랫폼 (WEB / ANDROID / IOS) | Y |

**Platform**
| 값 | 설명 |
|----|------|
| WEB | 웹 브라우저 |
| ANDROID | 안드로이드 앱 |
| IOS | iOS 앱 |

**요청 예시**
```json
{
  "token": "cmsVx8tgR0iZK5L9p0Q1x:APA91bFgA...",
  "platform": "IOS"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 등록 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[디바이스 토큰]이 성공적으로 등록되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 유효성 검증 실패 | 잘못된 요청 인자 |

**응답 예시**
```json
{
  "code": 400,
  "message": "잘못된 [인자]입니다.",
  "data": null
}
```
