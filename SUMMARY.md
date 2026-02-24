# Table of contents

* [SURF API Documentation](README.md)

## Auth (인증) <a href="#auth" id="auth"></a>

* [카카오 인가 화면 리다이렉트](auth/kakao-login.md)
* [카카오 로그인 콜백](auth/kakao-callback.md)
* [토큰 재발급](auth/refresh.md)
* [로그아웃](auth/logout.md)

## Member (회원) <a href="#member" id="member"></a>

* [회원가입](member/signup.md)
* [온보딩 상태 확인](member/onboarding-status.md)
* [회원 프로필 조회](member/profile.md)
* [회원 프로필 수정](member/profile-update.md)
* [회원 검색](member/search.md)
* [회원 수 조회](member/members-count.md)
* [기수 정보 조회](member/generations.md)
* [회원 탈퇴](member/withdraw.md)
* [회원가입 승인](member/approve-member.md)
* [회원가입 거절](member/reject-member.md)
* [회원 역할 변경 (단일)](member/role-change.md)
* [회원 역할 일괄 변경 (다중)](member/role-change-bulk.md)
* [관리자 회원 조회 (이름)](member/admin-search.md)
* [관리자 회원 조회 (트랙별)](member/admin-search-by-track.md)
* [가입신청 목록 조회](member/registration-list.md)
* [유저 상세 조회](member/member-detail.md)
* [승인된 회원 목록 조회](member/approved-members.md)
* [관리자 페이지 로그인](member/admin-login.md)
* [비밀번호 설정](member/admin-password.md)

## Board (게시판) <a href="#board" id="board"></a>

* [게시판 생성](board/create.md)
* [게시판 목록 조회](board/list.md)
* [게시판 단건 조회](board/detail.md)
* [게시판 수정](board/update.md)
* [게시판 삭제](board/delete.md)

## Post (게시글) <a href="#post" id="post"></a>

* [게시글 생성](post/create.md)
* [게시글 조회](post/detail.md)
* [게시판별 게시글 목록](post/list.md)
* [내가 작성한 게시글](post/my-posts.md)
* [특정 작성자 게시글](post/author-posts.md)
* [게시글 수정](post/update.md)
* [게시글 삭제](post/delete.md)
* [게시글 좋아요 설정](post/like.md)
* [게시글 좋아요 해제](post/unlike.md)
* [게시글 좋아요 목록 조회](post/like-list.md)
* [게시글 검색](post/search.md)
* [최근 검색어 조회](post/recent-search.md)
* [최근 검색어 전체 삭제](post/recent-search-delete-all.md)
* [최근 검색어 단건 삭제](post/recent-search-delete.md)

## Comment (댓글) <a href="#comment" id="comment"></a>

* [댓글 생성](comment/create.md)
* [댓글 목록 조회](comment/list.md)
* [댓글 삭제](comment/delete.md)
* [댓글 좋아요 토글](comment/like.md)
* [댓글 좋아요 수 조회](comment/like-count.md)
* [댓글 좋아요 여부 조회](comment/like-me.md)
* [댓글 좋아요 회원 목록](comment/like-members.md)
* [멘션 검색](comment/mention.md)

## Scrap (스크랩) <a href="#scrap" id="scrap"></a>

* [스크랩 추가](scrap/add.md)
* [스크랩 삭제](scrap/remove.md)
* [내 스크랩 목록](scrap/my-list.md)

## Letter (쪽지) <a href="#letter" id="letter"></a>

* [쪽지 전송](letter/send.md)
* [보낸 쪽지 목록](letter/sent-list.md)

## Home (홈) <a href="#home" id="home"></a>

* [홈 화면 조회](home/home.md)
* [홈 배너 목록 조회](home/banner-list.md)
* [홈 배너 생성](home/banner-create.md)
* [홈 배너 수정](home/banner-update.md)
* [홈 배너 삭제](home/banner-delete.md)
* [홈 배너 순서 변경](home/banner-reorder.md)
* [홈 배너 활성화](home/banner-activate.md)
* [홈 배너 비활성화](home/banner-deactivate.md)
* [홈 문구 조회](home/content.md)
* [홈 문구 수정](home/content-update.md)

## Badge (활동뱃지) <a href="#badge" id="badge"></a>

* [뱃지 부여](badge/create.md)
* [내 뱃지 조회](badge/my-list.md)

## Activity (활동기록) <a href="#activity" id="activity"></a>

* [활동기록 부여 (V1)](activity/create.md)
* [활동기록 부여 (V2)](activity/create-v2.md)
* [활동기록 조회](activity/list.md)
* [활동점수 조회](activity/score.md)
* [활동 종류 전체 조회](activity/types.md)
* [활동 카테고리 목록 조회](activity/categories.md)
* [특정 카테고리 활동 종류 조회](activity/type-by-category.md)
* [관리자 회원 활동기록 조회](activity/admin-member-records.md)
* [관리자 팀 활동기록 조회](activity/admin-team-records.md)
* [관리자 활동기록 수정](activity/admin-update.md)
* [관리자 활동기록 삭제](activity/admin-delete.md)

## Score (점수 현황) <a href="#score" id="score"></a>

* [활동점수 + 고정 활동기록 조회](score/personal.md)
* [개인별 상/벌점 현황 조회](score/ranking.md)
* [팀별 상/벌점 현황 조회](score/team-ranking.md)
* [특정 팀 멤버별 점수 조회](score/team-members.md)

## Team (팀) <a href="#team" id="team"></a>

* [팀 생성](team/create.md)
* [팀 목록 조회](team/list.md)
* [팀 상세 조회](team/detail.md)
* [팀 수정](team/update.md)
* [팀 삭제](team/delete.md)

## Feedback (피드백) <a href="#feedback" id="feedback"></a>

* [피드백 생성](feedback/create.md)
* [피드백 조회](feedback/list.md)

## Notification (알림) <a href="#notification" id="notification"></a>

* [알림 조회](notification/list.md)
* [알림 읽음 처리](notification/read.md)
* [FCM 토큰 등록](notification/device-token.md)
* [FCM 푸시 알림 테스트](notification/test-push.md)

## Schedule (일정) <a href="#schedule" id="schedule"></a>

* [월별 일정 조회](schedule/calendar.md)
* [일정 단건 조회](schedule/detail.md)
* [개별 일정 생성](schedule/create.md)
* [게시글 일정 조회](schedule/post-schedule.md)
* [게시글 일정 생성](schedule/post-schedule-create.md)
* [게시글 매핑 일정 삭제](schedule/post-schedule-delete.md)
* [일정 수정](schedule/update.md)
* [일정 삭제](schedule/delete.md)

## File (파일 업로드) <a href="#file" id="file"></a>

* [PreSigned URL 생성](file/presigned-url.md)
