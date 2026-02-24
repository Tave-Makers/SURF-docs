## 게시글 매핑 일정 삭제

### 개요
게시글에 매핑된 일정을 삭제합니다. 일정 삭제와 함께 게시글의 hasSchedule을 false로, scheduleId를 null로 업데이트합니다.

### 엔드포인트
`DELETE /v1/admin/posts/{postId}/schedules/{scheduleId}`

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
| postId | Long | 게시글 ID | O |
| scheduleId | Long | 일정 ID | O |

**요청 예시**
```
DELETE /v1/admin/posts/12/schedules/5
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 200 OK | 게시글 매핑 일정 삭제 성공 |

**응답 예시**
```json
{
  "code": 200,
  "message": "[일정]이 성공적으로 삭제되었습니다."
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 404 Not Found | 리소스 없음 | 일정 또는 게시글이 존재하지 않음 |

**응답 예시**
```json
{
  "code": 404,
  "message": "존재하지 않는 [일정]입니다.",
  "data": null
}
```

---

### 비즈니스 로직
- 일정 삭제 시 연동된 게시글의 `hasSchedule`을 `false`로 업데이트
- 연동된 게시글의 `scheduleId`를 `null`로 업데이트
