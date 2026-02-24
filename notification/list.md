## 알림 조회

### 개요
현재 사용자의 알림을 조회합니다. category로 필터링할 수 있습니다.

### 엔드포인트
`GET /v1/user/notifications`

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

**Query Parameters**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| category | String | 알림 카테고리 필터 (ACTIVITY / SCHEDULE) | N |

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 조회 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| data[] | Array | 알림 목록 |
| data[].id | Long | 알림 ID |
| data[].type | String | 알림 유형 (아래 NotificationType 참조) |
| data[].category | String | 카테고리 (ACTIVITY / SCHEDULE) |
| data[].body | String | 알림 본문 |
| data[].deepLink | String | 클릭 시 이동할 딥링크 |
| data[].read | Boolean | 읽음 여부 |
| data[].createdAt | String | 생성 시간 |

**NotificationType**
| 타입 | 카테고리 | 설명 |
|------|---------|------|
| POST_LIKE | ACTIVITY | 게시글 좋아요 |
| POST_COMMENT | ACTIVITY | 게시글 댓글 |
| COMMENT_LIKE | ACTIVITY | 댓글 좋아요 |
| COMMENT_REPLY | ACTIVITY | 댓글 답글 |
| MESSAGE | ACTIVITY | 쪽지 수신 |
| BADGE_UPDATE | ACTIVITY | 뱃지 업데이트 |
| SCORE_UPDATE | ACTIVITY | 점수 업데이트 |
| NOTICE | SCHEDULE | 공지사항 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[알람]이 성공적으로 조회되었습니다.",
  "data": [
    {
      "id": 5,
      "type": "POST_LIKE",
      "category": "ACTIVITY",
      "body": "홍길동님이 회원님의 게시글에 좋아요를 남겼습니다.",
      "deepLink": "board/1/post/2",
      "read": false,
      "createdAt": "2025-10-05T14:48:00"
    },
    {
      "id": 3,
      "type": "NOTICE",
      "category": "SCHEDULE",
      "body": "[공지사항] 새로운 공지사항이 업데이트 되었습니다",
      "deepLink": "board/1/post/1",
      "read": true,
      "createdAt": "2025-10-05T14:46:00"
    }
  ]
}
```
