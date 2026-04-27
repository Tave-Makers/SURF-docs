## 게시판 카테고리 생성

### 개요
게시판 카테고리 생성

### 엔드포인트
`POST /v1/admin/boards/{boardId}/categories`

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
| boardId | Long | boardId | O |

**Body (BoardCategoryCreateReqDTO)**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| 이름" | "카테고리 | 이름" | X |
| name | String | name | O |
| slug | String | slug | O |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 요청 성공 |

**Body (BoardCategoryResDTO)**
| Key | Type | 설명 |
|-----|------|------|
| ID" | "카테고리 | ID" |
| id | Long | id |
| 이름" | "카테고리 | 이름" |
| name | String | name |
| "슬러그" | = | "슬러그" |
| slug | String | slug |

**응답 예시**
```json
{
  "code": 201,
  "message": "요청이 성공적으로 처리되었습니다.",
  "data": null
}
```
