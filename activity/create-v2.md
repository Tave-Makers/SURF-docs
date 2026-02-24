## 활동기록 부여 V2 (Manager)

### 개요
인증된 사용자(매니저)가 개인 또는 팀 단위로 활동 점수(기록)를 부여합니다. V1과 달리 팀 점수 부여를 지원하며, `memberIdList`와 `teamIdList` 중 하나만 전달해야 합니다.

### 엔드포인트
`POST /v1/manager/activity-records`

### 인증
- **인증 필요 여부:** JWT 인증 필요
- **권한:** 인증된 사용자 접근 가능 (로그인 필요)

> 요청 헤더(Header)에 아래와 같이 Authorization 필드를 포함해야 합니다.
> `Authorization: Bearer {JWT_TOKEN}`

### 요청 (Request)

**Headers**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| Authorization | String | Bearer 토큰 | O |

**Body**
| Key | Type | 설명 | 필수 |
|-----|------|------|------|
| memberIdList | Array\<Long\> | 대상 회원 ID 목록 (개인 점수 부여 시) | 조건부 |
| teamIdList | Array\<Long\> | 대상 팀 ID 목록 (팀 점수 부여 시) | 조건부 |
| category | String | 활동 카테고리 (ActivityCategory enum) | X |
| appliedTarget | String | 적용 대상 (`TEAM` 또는 `INDIVIDUAL`) | X |
| activityName | String | 활동 유형 (ActivityType enum, 아래 참조) | O |
| activityDate | String | 활동을 수행한 날짜 (YYYY-MM-DD) | O |

> `memberIdList`와 `teamIdList`는 둘 중 하나만 존재해야 합니다. 둘 다 존재하거나 둘 다 비어 있으면 유효성 검증에 실패합니다.

**요청 예시 - 개인 점수 부여**
```json
{
  "memberIdList": [1, 2, 3],
  "teamIdList": null,
  "appliedTarget": "INDIVIDUAL",
  "activityName": "EARLY_BIRD",
  "activityDate": "2025-02-24"
}
```

**요청 예시 - 팀 점수 부여**
```json
{
  "memberIdList": null,
  "teamIdList": [10, 11],
  "appliedTarget": "TEAM",
  "activityName": "DO_NOT_UPLOAD_CLERK_ON_TEAM",
  "activityDate": "2025-02-24"
}
```

---

### 응답 (Response)

**성공**
| HTTP Status | 의미 |
|-------------|------|
| 201 Created | 부여 성공 |

**응답 예시**
```json
{
  "code": 201,
  "message": "[활동 기록]을 적용했습니다.",
  "data": null
}
```

---

### 실패 (Error)
| HTTP Status | 의미 | 설명 |
|-------------|------|------|
| 400 Bad Request | 요청 실패 | memberIdList와 teamIdList 둘 중 하나만 존재해야 함 |
| 401 Unauthorized | 인증 실패 | JWT 토큰 누락 또는 만료 |
| 403 Forbidden | 권한 부족 | 인증된 사용자 권한 필요 |

---

## 참고: ActivityType (활동 유형) 목록

### 상점 (REWARD) - 개인 적용

| 값 | 설명 | 점수 | 카테고리 |
|----|------|------|----------|
| EARLY_BIRD | 행사 얼리버드 | +5 | 정규 행사 |
| ENGAGE_AFTER_PARTY | 뒷풀이 참여 | +5 | 활동 |
| CREATE_FLASH_MEETUP | 번개모임 주최 | +10 | 활동 |
| ENGAGE_FLASH_MEETUP | 번개모임 참여 | +5 | 활동 |
| SHARE_INFORMATION_AGIT | 아지트 정보 공유 | +3 | 활동 |
| ENGAGE_TECH_SEMINAR | 기술 세미나 참여 | +10 | 활동 |
| PRESENT_OUTLINE | 기획안 발표 | +10 | 활동 |
| CREATE_SOCIAL_CLUB | 소모임 생성 | +15 | 활동 |
| ENGAGE_SOCIAL_CLUB | 소모임 활동 | +3 | 활동 |
| WRITE_WIL | WIL 작성 | +3 | 활동 |
| UPLOAD_INSTAGRAM_STORY | 인스타그램 스토리 업로드 | +3 | 활동 |
| UPLOAD_TAVE_REVIEW | TAVE 활동 후기 업로드 | +20 | 활동 |
| TEAM_LEADER | 팀장 역할 수행 | +10 | 활동 |

### 벌점 (PENALTY) - 개인 적용

| 값 | 설명 | 점수 | 카테고리 |
|----|------|------|----------|
| SESSION_ABSENCE | 정규 세션 결석 | -30 | 정규 행사 |
| SESSION_TRUANCY | 정규 세션 무단 결석 | -100 | 정규 행사 |
| SESSION_LATE | 정규 세션 지각 | 0 | 정규 행사 |
| SESSION_LATE_1_TO_10 | 정규 세션 지각 (1~10분) | -10 | 정규 행사 |
| SESSION_LATE_11_TO_20 | 정규 세션 지각 (11~20분) | -20 | 정규 행사 |
| SESSION_LATE_21_TO_30 | 정규 세션 지각 (21~30분) | -30 | 정규 행사 |
| TEAM_LATE | 스터디/프로젝트 지각 | 0 | 스터디(개인) |
| STUDY_LATE_6_TO_10 | 스터디 지각 (6~10분) | -5 | 스터디(개인) |
| STUDY_LATE_11_TO_20 | 스터디 지각 (11~20분) | -10 | 스터디(개인) |
| STUDY_LATE_21_TO_30 | 스터디 지각 (21~30분) | -15 | 스터디(개인) |
| STUDY_ABSENCE | 스터디 결석 | -30 | 스터디(개인) |
| PROJECT_LATE_6_TO_10 | 프로젝트 지각 (6~10분) | -5 | 프로젝트(개인) |
| PROJECT_LATE_11_TO_20 | 프로젝트 지각 (11~20분) | -10 | 프로젝트(개인) |
| PROJECT_LATE_21_TO_30 | 프로젝트 지각 (21~30분) | -15 | 프로젝트(개인) |
| PROJECT_ABSENCE | 프로젝트 결석 | -30 | 프로젝트(개인) |
| TEAM_ABSENCE | 스터디/프로젝트 결석 | 0 | 프로젝트(개인) |
| NO_VOTE | 투표 미참여 | -15 | 활동 |
| DELAY_DEPOSIT | 보증금 입금 지연 | -5 | 활동 |
| NO_SHOW_AFTER_PARTY | 뒷풀이 불참 | -10 | 활동 |

### 벌점 (PENALTY) - 팀 적용

| 값 | 설명 | 점수 | 카테고리 |
|----|------|------|----------|
| PROJECT_LATE_6_TO_10_ON_TEAM | 프로젝트 지각 (6~10분) | -5 | 프로젝트(팀) |
| PROJECT_LATE_11_TO_20_ON_TEAM | 프로젝트 지각 (11~20분) | -10 | 프로젝트(팀) |
| PROJECT_LATE_21_TO_30_ON_TEAM | 프로젝트 지각 (21~30분) | -15 | 프로젝트(팀) |
| STUDY_LATE_6_TO_10_ON_STUDY | 스터디 지각 (6~10분) | -5 | 스터디(팀) |
| STUDY_LATE_11_TO_20_ON_STUDY | 스터디 지각 (11~20분) | -10 | 스터디(팀) |
| STUDY_LATE_21_TO_30_ON_STUDY | 스터디 지각 (21~30분) | -15 | 스터디(팀) |
| LATE_CLERK_UPLOAD_ON_TEAM | 서기 업로드 지각 | -10 | 프로젝트(팀) |
| LATE_PROGRESS_TABLE_UPLOAD_ON_TEAM | 진행표 업로드 지각 | -10 | 프로젝트(팀) |
| DO_NOT_UPLOAD_CLERK_ON_TEAM | 서기 미제출 | -30 | 프로젝트(팀) |
| DO_NOT_UPLOAD_PROGRESS_TABLE_ON_TEAM | 진행표 미제출 | -30 | 프로젝트(팀) |
| LATE_UPLOAD_CERTIFICATION_PHOTO_ON_TEAM | 사진 업로드 지각 | -5 | 프로젝트(팀) |
| LATE_SCHEDULE_ALERT_ON_TEAM | 일정 공지 지각 | -5 | 프로젝트(팀) |
| LATE_SUBMIT_FINAL_PRODUCT_ON_TEAM | 결과물 제출 지각 | -30 | 프로젝트(팀) |
| DO_NOT_ALERT_ABSENCE_OF_PERSONAL_REASON_ON_TEAM | 개인 사유로 인한 결석 미공지 | -10 | 프로젝트(팀) |
| DO_NOT_ALERT_TARDINESS_OF_PERSONAL_REASON_ON_TEAM | 개인 사유로 인한 지각 미공지 | -10 | 프로젝트(팀) |
| LATE_CLERK_UPLOAD_ON_STUDY | 서기 업로드 지각 | -10 | 스터디(팀) |
| LATE_PROGRESS_TABLE_UPLOAD_ON_STUDY | 진행표 업로드 지각 | -10 | 스터디(팀) |
| DO_NOT_UPLOAD_CLERK_ON_STUDY | 서기 미제출 | -30 | 스터디(팀) |
| DO_NOT_UPLOAD_PROGRESS_TABLE_ON_STUDY | 진행표 미제출 | -30 | 스터디(팀) |
| LATE_UPLOAD_CERTIFICATION_PHOTO_ON_STUDY | 사진 업로드 지각 | -5 | 스터디(팀) |
| LATE_SCHEDULE_ALERT_ON_STUDY | 일정 공지 지각 | -5 | 스터디(팀) |
| LATE_SUBMIT_FINAL_PRODUCT_ON_STUDY | 결과물 제출 지각 | -30 | 스터디(팀) |
| DO_NOT_ALERT_ABSENCE_OF_PERSONAL_REASON_ON_STUDY | 개인 사유로 인한 결석 미공지 | -10 | 스터디(팀) |
| DO_NOT_ALERT_TARDINESS_OF_PERSONAL_REASON_ON_STUDY | 개인 사유로 인한 지각 미공지 | -10 | 스터디(팀) |

### AppliedTarget (적용 대상)
| 값 | 설명 |
|----|------|
| INDIVIDUAL | 개인 점수에 적용 |
| TEAM | 팀 점수에 적용 |

### ActivityCategory (활동 카테고리)
| 값 | 표시명 |
|----|--------|
| STUDY_ON_PERSONAL | 스터디(개인) |
| PROJECT_ON_PERSONAL | 프로젝트(개인) |
| STUDY_ON_TEAM | 스터디(팀) |
| PROJECT_ON_TEAM | 프로젝트(팀) |
| REGULAR_SESSION | 정규 행사 |
| ACTIVITY | 활동 |
