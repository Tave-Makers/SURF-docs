## 홈 문구 관리

---

### 1. 홈 문구 조회

#### 개요
홈 화면에 표시되는 메인 문구를 조회합니다.

#### 엔드포인트
`GET /v1/admin/home/content`

#### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | Y |

---

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| mainText | String | 홈 메인 문구 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 문구]가 성공적으로 조회되었습니다.",
  "data": {
    "mainText": "TAVE와 함께 성장하세요!"
  }
}
```

---

### 2. 홈 문구 수정

#### 개요
홈 화면 메인 문구를 생성하거나 수정합니다. 항상 단일 레코드(id=1)로 관리됩니다.

#### 엔드포인트
`PUT /v1/admin/home/content`

#### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `ADMIN`, `PRESIDENT`, `MANAGER`

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

#### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | Y |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| mainText | String | 메인 문구 (최대 2000자) | Y |

**요청 예시**
```json
{
  "mainText": "TAVE와 함께 성장하세요!"
}
```

---

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 수정 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 문구]가 성공적으로 수정되었습니다.",
  "data": null
}
```
