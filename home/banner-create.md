## 배너 생성

### 개요
새로운 홈 배너를 생성합니다.

### 엔드포인트
`POST /v1/admin/home/banners`

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
| imageUrl | String | 배너 이미지 URL (최대 1000자) | Y |
| linkUrl | String | 배너 클릭 시 이동 URL | N |

**요청 예시**
```json
{
  "imageUrl": "https://s3.../banner2.jpg",
  "linkUrl": "https://tavesurf.site/event"
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
| id | Long | 배너 ID |
| imageUrl | String | 배너 이미지 URL |
| linkUrl | String | 배너 클릭 시 이동 URL |
| displayOrder | Integer | 배너 표시 순서 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[홈 배너]가 성공적으로 생성되었습니다.",
  "data": {
    "id": 2,
    "imageUrl": "https://s3.../banner2.jpg",
    "linkUrl": null,
    "displayOrder": 2
  }
}
```
