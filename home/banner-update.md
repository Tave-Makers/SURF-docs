## 배너 수정

### 개요
특정 배너를 수정합니다.

### 엔드포인트
`PUT /v1/admin/home/banners/{bannerId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| bannerId | Long | 배너 ID | Y |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| imageUrl | String | 배너 이미지 URL | Y |
| linkUrl | String | 배너 클릭 시 이동 URL | N |

**요청 예시**
```json
{
  "imageUrl": "https://s3.../banner_updated.jpg",
  "linkUrl": "https://tavesurf.site/updated"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 수정 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 배너]가 성공적으로 수정되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 배너 없음 | 해당 배너를 찾을 수 없음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [홈 배너]입니다.",
  "data": null
}
```
