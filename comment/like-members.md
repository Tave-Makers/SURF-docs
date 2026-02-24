## 댓글 좋아요 누른 회원 목록 조회

### 개요
특정 댓글에 좋아요를 누른 회원 목록을 조회합니다.

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 일반 사용자 접근 가능 (MEMBER 이상)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

---

### 엔드포인트
`GET /v1/user/comments/{commentId}/like/members`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Path Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| commentId | Long | 댓글 ID | O |

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| memberId | Long | 회원 ID |
| nickname | String | 닉네임 |
| profileImageUrl | String | 프로필 이미지 URL |

**응답 예시**
```json
{
  "code": 200,
  "message": "[댓글 좋아요] 누른 회원 목록이 성공적으로 조회되었습니다.",
  "data": [
    {
      "memberId": 5,
      "nickname": "홍길동",
      "profileImageUrl": "https://example.com/profile.jpg"
    }
  ]
}
```
