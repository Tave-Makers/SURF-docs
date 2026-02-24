## 배너 비활성화

### 개요
특정 배너를 비활성화합니다.

### 엔드포인트
`PATCH /v1/admin/home/banners/{id}/deactivate`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 관리자만 접근 가능 (MANAGER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| id | Long | 배너 ID | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 비활성화 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| id | Long | 배너 ID |
| name | String | 배너 이름 |
| imageUrl | String | 배너 이미지 URL |
| linkUrl | String | 배너 클릭 시 이동 URL |
| displayOrder | Integer | 배너 표시 순서 |
| status | Boolean | 배너 활성 상태 (false) |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 배너]를 비활성화했습니다.",
  "data": {
    "id": 1,
    "name": "새로운 17기 환영 배너",
    "imageUrl": "https://s3.../banner1.jpg",
    "linkUrl": "https://tavesurf.site/event",
    "displayOrder": 1,
    "status": false
  }
}
```

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
