## 홈 화면 조회

### 개요
홈 화면에 필요한 배너, 문구, 최근 게시글 등의 데이터를 조회합니다.

### 엔드포인트
`GET /v1/user/home`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

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
| banners | Array | 배너 목록 |
| banners[].id | Long | 배너 ID |
| banners[].imageUrl | String | 배너 이미지 URL |
| banners[].linkUrl | String | 배너 클릭 시 이동 URL |
| banners[].displayOrder | Integer | 배너 표시 순서 |
| mainText | String | 홈 메인 문구 |
| recentPosts | Array | 최근 게시글 목록 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[홈 화면] 데이터가 성공적으로 조회되었습니다.",
  "data": {
    "banners": [
      {
        "id": 1,
        "imageUrl": "https://s3.../banner1.jpg",
        "linkUrl": "https://tavesurf.site/event",
        "displayOrder": 1
      }
    ],
    "mainText": "TAVE와 함께 성장하세요!",
    "recentPosts": [...]
  }
}
```
