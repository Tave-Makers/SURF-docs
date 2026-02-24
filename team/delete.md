## 팀 삭제

### 개요
특정 ID의 팀을 삭제합니다. 팀에 소속된 팀원(TeamMember) 관계도 함께 삭제됩니다.

### 엔드포인트
`DELETE /v1/admin/teams/{teamId}`

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
| teamId | Long | 삭제할 팀의 ID | O |

**요청 예시**
```
DELETE /v1/admin/teams/1
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 204 No Content | 팀 삭제 성공 |

**Body**
| Key | Type | 설명 |
|-----|------|------|
| code | Integer | HTTP 상태 코드 |
| message | String | 응답 메시지 |
| data | null | 응답 데이터 없음 |

**응답 예시**
```json
{
  "code": 204,
  "message": "[팀]이 성공적으로 삭제되었습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 401 Unauthorized | 인증 실패 | JWT 토큰이 유효하지 않음 |
| 403 Forbidden | 권한 부족 | 관리자 권한이 없음 |
| 404 Not Found | 팀 없음 | 존재하지 않는 [팀]입니다. |
