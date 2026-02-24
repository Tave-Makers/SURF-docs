## 홈 배너 관리

---

### 1. 배너 목록 조회

#### 개요
홈 배너 목록을 조회합니다.

#### 엔드포인트
`GET /v1/admin/home/banners`

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

---

### 2. 배너 생성

#### 개요
새로운 홈 배너를 생성합니다.

#### 엔드포인트
`POST /v1/admin/home/banners`

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

#### 응답 (Response)

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

---

### 3. 배너 수정

#### 개요
특정 배너를 수정합니다.

#### 엔드포인트
`PUT /v1/admin/home/banners/{bannerId}`

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

#### 응답 (Response)

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

#### 실패 (Error)
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

---

### 4. 배너 삭제

#### 개요
특정 배너를 삭제합니다.

#### 엔드포인트
`DELETE /v1/admin/home/banners/{bannerId}`

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

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| bannerId | Long | 배너 ID | Y |

---

#### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 삭제 성공 |

---

#### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 배너 없음 | 해당 배너를 찾을 수 없음 |

---

### 5. 배너 순서 변경

#### 개요
배너 순서를 변경합니다. 모든 배너 ID를 원하는 순서대로 배열로 전달해야 합니다.

#### 엔드포인트
`PUT /v1/admin/home/banners/reorder`

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
| bannerIds | Array\<Long\> | 배너 ID 배열 (원하는 순서대로) | Y |

**요청 예시**
```json
{
  "bannerIds": [3, 1, 2]
}
```

---

#### 응답 (Response)

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

#### 실패 (Error)
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
