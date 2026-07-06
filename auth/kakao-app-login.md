## 카카오 앱 SDK 로그인

### 개요
카카오 앱 SDK 로그인

### 엔드포인트
`POST /login/kakao/app`

### 인증
- **인증 필요 여부:** 불필요
- **권한:** 인증 불필요

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Body (KakaoAppLoginReqDTO)**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| accessToken | String | accessToken | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 요청 성공 |

**Body (LoginResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| 닉네임" | "사용자 | 닉네임" |
| nickname | String | nickname |
| 이메일" | "사용자 | 이메일" |
| email | String | email |
| accessToken | String | accessToken |
| 포함 | 클라이언트만 | 포함 |
| refreshToken | String | refreshToken |
| URL" | 이미지 | URL" |
| profileImageUrl | String | profileImageUrl |

**응답 예시**
```json
{
  "code": 200,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
