## 배너 목록 조회

### 개요
홈 배너 목록을 조회합니다.

### 엔드포인트
`GET /v1/admin/home/banners`

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

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| data[] | Array | 배너 목록 |
| data[].id | Long | 배너 ID |
| data[].imageUrl | String | 배너 이미지 URL |
| data[].linkUrl | String | 배너 클릭 시 이동 URL |
| data[].displayOrder | Integer | 배너 표시 순서 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 배너]가 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 1,
      "imageUrl": "https://s3.../banner1.jpg",
      "linkUrl": "https://tavesurf.site/event",
      "displayOrder": 1
    }
  ]
}
```
