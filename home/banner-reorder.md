## 배너 순서 변경

### 개요
배너 순서를 변경합니다. 모든 배너 ID를 원하는 순서대로 배열로 전달해야 합니다.

### 엔드포인트
`PUT /v1/admin/home/banners/reorder`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

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
| bannerIds | Array\<Long\> | 배너 ID 배열 (원하는 순서대로) | Y |

**요청 예시**
```json
{
  "bannerIds": [3, 1, 2]
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 순서 변경 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 배너] 순서가 성공적으로 변경되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 배너 목록 불일치 | 전달된 배너 ID 목록이 실제 배너 목록과 일치하지 않음 |

**응답 예시**
```json
{
  "code": 400,
  "message": "모든 [홈 배너]를 입력해야 합니다.",
  "data": null
}
```
