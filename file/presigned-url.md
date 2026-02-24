## PreSigned URL 생성

### 개요
AWS S3에 파일을 업로드하기 위한 PreSigned URL을 생성합니다. URL 유효 시간은 2분입니다.

### 엔드포인트
`POST /v1/user/presigned-url`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** `MEMBER`, `ADMIN`, `PRESIDENT`, `MANAGER`

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
| fileNames | Array\<String\> | 업로드할 파일명 배열 (최소 1개) | Y |

**요청 예시**
```json
{
  "fileNames": ["profile_image.jpg", "post_image.png"]
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 생성 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| data[] | Array | PreSigned URL 목록 |
| data[].key | String | S3 파일 키 (경로) |
| data[].preSignedUrl | String | 파일 업로드용 PreSigned URL |
| data[].originalFileName | String | 원본 파일명 |

> S3 키 구조: `original/{UUID}/{originalFileName}`
> PreSigned URL 유효 시간: 2분

**응답 예시**
```json
{
  "code": 200,
  "message": "[PreSignedUrl]을 발급했습니다.",
  "data": [
    {
      "key": "original/550e8400-e29b-41d4-a716-446655440000/profile_image.jpg",
      "preSignedUrl": "https://bucket.s3.amazonaws.com/original/550e8400.../profile_image.jpg?X-Amz-Algorithm=...",
      "originalFileName": "profile_image.jpg"
    }
  ]
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 파일명 없음 | 전달받은 파일명이 없음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "건네받은 [파일명]이 없습니다.",
  "data": null
}
```

---

### 클라이언트 업로드 방법

PreSigned URL을 받은 후 클라이언트에서 직접 S3에 업로드합니다:

```bash
curl -X PUT \
  --data-binary @"profile_image.jpg" \
  -H "Content-Type: image/jpeg" \
  "{preSignedUrl}"
```
