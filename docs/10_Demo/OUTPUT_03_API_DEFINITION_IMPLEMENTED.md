# Output 03 - API Definition (Implemented Features)

- Generated: 2026-02-24
- Source: Spring controllers + Django internal urls/views

## Summary

- Spring endpoints: **86** (external 84, internal 2)
- Django internal endpoints: **2**
- Total endpoints: **88**

## Domain Counts

### External Domain Counts (Spring external: 84)

| Domain | Count |
|---|---:|
| `account` | 6 |
| `auth` | 12 |
| `challenge` | 18 |
| `common` | 3 |
| `meeting` | 8 |
| `notification` | 6 |
| `post` | 15 |
| `system` | 4 |
| `user` | 7 |
| `vote` | 5 |

### Internal Domain Counts (Spring + Django internal: 4)

| Domain | Count |
|---|---:|
| `brix` (Spring internal) | 1 |
| `common` (Spring internal) | 1 |
| `django` (Django internal) | 2 |

## External API Table

### account (6)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| POST | `/accounts/charge` | Authorization header(optional in annotation; may be validated in service) |  |  | CreditChargeRequest | `ApiResponse<CreditChargeResponse` | `AccountController.requestCreditCharge` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:67` |
| POST | `/accounts/charge/callback` | Public/No header |  |  | ChargeCallbackRequest | `ApiResponse<ChargeCallbackResponse` | `AccountController.processChargeCallback` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:80` |
| GET | `/accounts/me` | Authorization header(optional in annotation; may be validated in service) |  |  |  | `ApiResponse<MyAccountResponse` | `AccountController.getMyAccount` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:113` |
| GET | `/accounts/me/transactions` | Authorization header(optional in annotation; may be validated in service) |  | endDate, page, size, startDate, type |  | `ApiResponse<TransactionHistoryResponse` | `AccountController.getTransactionHistory` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:42` |
| POST | `/accounts/support` | Authorization header(optional in annotation; may be validated in service) |  |  | SupportRequest | `ApiResponse<SupportResponse` | `AccountController.requestSupport` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:104` |
| POST | `/accounts/withdraw` | Authorization header(optional in annotation; may be validated in service) |  |  | WithdrawRequest | `ApiResponse<WithdrawResponse` | `AccountController.requestWithdraw` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:91` |

### auth (12)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| POST | `/auth/email/confirm` | Public/No header |  |  | EmailConfirmRequest | `ApiResponse<EmailConfirmResponse` | `AuthController.confirmEmail` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:210` |
| POST | `/auth/email/verify` | Public/No header |  |  | EmailVerifyRequest | `ApiResponse<EmailVerifyResponse` | `AuthController.verifyEmail` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:199` |
| POST | `/auth/login` | Public/No header |  |  | LoginRequest | `ApiResponse<LoginResponse` | `AuthController.login` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:71` |
| POST | `/auth/logout` | Public/No header |  |  | LogoutRequest | `ApiResponse<LogoutResponse` | `AuthController.logout` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:225` |
| POST | `/auth/password/reset` | Public/No header |  |  | PasswordResetRequest | `ApiResponse<PasswordResetResponse` | `AuthController.requestPasswordReset` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:253` |
| PUT | `/auth/password/reset` | Public/No header |  |  | PasswordResetExecuteRequest | `ApiResponse<PasswordResetExecuteResponse` | `AuthController.resetPassword` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:272` |
| POST | `/auth/refresh` | Public/No header |  |  | RefreshRequest | `ApiResponse<RefreshResponse` | `AuthController.refresh` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:239` |
| POST | `/auth/signup` | Public/No header |  |  | SignupRequest | `ApiResponse<SignupResponse` | `AuthController.signup` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:89` |
| GET | `/auth/social/callback/{provider}` | Public/No header | provider | code, error, error_description, state |  | `Void` | `AuthController.socialProviderCallback` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:161` |
| POST | `/auth/social/complete` | Public/No header |  |  | SocialAuthCompleteRequest | `ApiResponse<LoginResponse` | `AuthController.completeSocialAuth` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:132` |
| GET | `/auth/social/providers` | Public/No header |  |  |  | `ApiResponse<SocialProviderStatusResponse` | `AuthController.getSocialProviderStatuses` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:126` |
| POST | `/auth/social/start` | Public/No header |  |  | SocialAuthStartRequest | `ApiResponse<SocialAuthStartResponse` | `AuthController.startSocialAuth` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:106` |

### challenge (18)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/challenges` | Public/No header |  |  |  | `ApiResponse<ChallengeListResponse` | `ChallengeController.getChallengeList` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:58` |
| POST | `/challenges` | Bearer Authorization |  |  | CreateChallengeRequest | `ApiResponse<CreateChallengeResponse` | `ChallengeController.createChallenge` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:258` |
| GET | `/challenges/me` | Bearer Authorization |  |  |  | `ApiResponse<MyChallengesResponse` | `ChallengeController.getMyChallenges` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:84` |
| DELETE | `/challenges/{challengeId}` | Bearer Authorization | challengeId |  |  | `ApiResponse<ChallengeDeleteResponse` | `ChallengeController.deleteChallenge` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:351` |
| GET | `/challenges/{challengeId}` | Authorization header(optional in annotation; may be validated in service) | challengeId |  |  | `ApiResponse<ChallengeDetailResponse` | `ChallengeController.getChallengeDetail` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:105` |
| PUT | `/challenges/{challengeId}` | Bearer Authorization | challengeId |  | UpdateChallengeRequest | `ApiResponse<UpdateChallengeResponse` | `ChallengeController.updateChallenge` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:218` |
| GET | `/challenges/{challengeId}/account` | Bearer Authorization | challengeId |  |  | `ApiResponse<ChallengeAccountResponse` | `ChallengeController.getChallengeAccount` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:130` |
| GET | `/challenges/{challengeId}/account/graph` | Bearer Authorization | challengeId | months |  | `ApiResponse<ChallengeLedgerGraphResponse` | `ChallengeController.getChallengeAccountGraph` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:154` |
| POST | `/challenges/{challengeId}/delegate` | Bearer Authorization | challengeId |  | DelegateLeaderRequest | `ApiResponse<DelegateLeaderResponse` | `ChallengeController.delegateLeader` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:442` |
| POST | `/challenges/{challengeId}/join` | Bearer Authorization | challengeId |  |  | `ApiResponse<JoinChallengeResponse` | `ChallengeController.joinChallenge` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:186` |
| DELETE | `/challenges/{challengeId}/leave` | Bearer Authorization | challengeId |  |  | `ApiResponse<LeaveChallengeResponse` | `ChallengeController.leaveChallenge` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:298` |
| GET | `/challenges/{challengeId}/ledger` | Bearer Authorization | challengeId | page, size |  | `ApiResponse<LedgerListResponse` | `LedgerController.getLedger` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:27` |
| POST | `/challenges/{challengeId}/ledger` | Bearer Authorization | challengeId |  | CreateLedgerEntryRequest | `ApiResponse<LedgerEntryResponse` | `LedgerController.createLedgerEntry` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:55` |
| GET | `/challenges/{challengeId}/ledger/summary` | Bearer Authorization | challengeId |  |  | `ApiResponse<LedgerSummaryResponse` | `LedgerController.getLedgerSummary` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:42` |
| GET | `/challenges/{challengeId}/members` | Bearer Authorization | challengeId |  |  | `ApiResponse<ChallengeMemberListResponse` | `ChallengeController.getChallengeMembers` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:325` |
| GET | `/challenges/{challengeId}/members/{memberId}` | Bearer Authorization | challengeId, memberId |  |  | `ApiResponse<com.woorido.challenge.dto.response.ChallengeMemberDetailResponse` | `ChallengeController.getMemberDetail` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:412` |
| PUT | `/challenges/{challengeId}/support/settings` | Bearer Authorization | challengeId |  | UpdateSupportSettingsRequest | `ApiResponse<UpdateSupportSettingsResponse` | `ChallengeController.updateSupportSettings` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:381` |
| PUT | `/ledger/{entryId}` | Bearer Authorization | entryId |  | UpdateLedgerEntryRequest | `ApiResponse<LedgerEntryResponse` | `LedgerController.updateLedgerEntry` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:69` |

### common (3)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| POST | `/uploads/challenges/banner` | Authorization header(optional in annotation; may be validated in service) |  | file |  | `ApiResponse<ImageUploadResponse` | `ImageUploadController.uploadChallengeBanner` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:28` |
| POST | `/uploads/challenges/thumbnail` | Authorization header(optional in annotation; may be validated in service) |  | file |  | `ApiResponse<ImageUploadResponse` | `ImageUploadController.uploadChallengeThumbnail` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:49` |
| POST | `/users/me/profile-image` | Authorization header(optional in annotation; may be validated in service) |  | file |  | `ApiResponse<ImageUploadResponse` | `ImageUploadController.uploadMyProfileImage` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:70` |

### meeting (8)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/challenges/{challengeId}/meetings` | Bearer Authorization | challengeId |  |  | `ApiResponse<MeetingListResponse` | `MeetingController.getMeetingList` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:32` |
| POST | `/challenges/{challengeId}/meetings` | Bearer Authorization | challengeId |  | CreateMeetingRequest | `ApiResponse<Object` | `MeetingController.createMeeting` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:57` |
| DELETE | `/meetings/{meetingId}` | Bearer Authorization | meetingId |  |  | `ApiResponse<Object` | `MeetingController.deleteMeeting` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:110` |
| GET | `/meetings/{meetingId}` | Bearer Authorization | meetingId |  |  | `ApiResponse<Object` | `MeetingController.getMeetingDetail` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:45` |
| PUT | `/meetings/{meetingId}` | Bearer Authorization | meetingId |  | UpdateMeetingRequest | `ApiResponse<Object` | `MeetingController.updateMeeting` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:71` |
| DELETE | `/meetings/{meetingId}/attendance` | Bearer Authorization | meetingId |  |  | `ApiResponse<Object` | `MeetingController.cancelAttendance` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:122` |
| POST | `/meetings/{meetingId}/attendance` | Bearer Authorization | meetingId |  | com.woorido.meeting.dto.request.AttendanceResponseRequest | `ApiResponse<Object` | `MeetingController.respondAttendance` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:84` |
| POST | `/meetings/{meetingId}/complete` | Bearer Authorization | meetingId |  | com.woorido.meeting.dto.request.CompleteMeetingRequest | `ApiResponse<Object` | `MeetingController.completeMeeting` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:97` |

### notification (6)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/notifications` | Authorization header(optional in annotation; may be validated in service) |  | isRead, page, size, type |  | `ApiResponse<NotificationListResponse` | `NotificationController.getNotifications` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:41` |
| PUT | `/notifications/read-all` | Authorization header(optional in annotation; may be validated in service) |  |  |  | `ApiResponse<NotificationReadAllResponse` | `NotificationController.markAllAsRead` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:112` |
| GET | `/notifications/settings` | Authorization header(optional in annotation; may be validated in service) |  |  |  | `ApiResponse<NotificationSettingsResponse` | `NotificationController.getSettings` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:128` |
| PUT | `/notifications/settings` | Authorization header(optional in annotation; may be validated in service) |  |  | UpdateNotificationSettingsRequest | `ApiResponse<NotificationSettingsResponse` | `NotificationController.updateSettings` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:140` |
| GET | `/notifications/{notificationId}` | Authorization header(optional in annotation; may be validated in service) | notificationId |  |  | `ApiResponse<NotificationResponse` | `NotificationController.getNotification` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:77` |
| PUT | `/notifications/{notificationId}/read` | Authorization header(optional in annotation; may be validated in service) | notificationId |  |  | `ApiResponse<NotificationMarkReadResponse` | `NotificationController.markAsRead` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:91` |

### post (15)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/challenges/{challengeId}/posts` | Authorization header(optional in annotation; may be validated in service) | challengeId | category, order, page, size, sortBy |  | `ApiResponse<PostListResponse` | `PostController.getPostList` | `backend/src/main/java/com/woorido/post/controller/PostController.java:144` |
| POST | `/challenges/{challengeId}/posts` | Authorization header(optional in annotation; may be validated in service) | challengeId |  | CreatePostRequest | `ApiResponse<CreatePostResponse` | `PostController.createPost` | `backend/src/main/java/com/woorido/post/controller/PostController.java:63` |
| POST | `/challenges/{challengeId}/posts/images` | Authorization header(optional in annotation; may be validated in service) | challengeId | files, files[] |  | `ApiResponse<PostImagesUploadResponse` | `PostController.uploadPostImages` | `backend/src/main/java/com/woorido/post/controller/PostController.java:381` |
| POST | `/challenges/{challengeId}/posts/upload` | Authorization header(optional in annotation; may be validated in service) | challengeId |  |  | `ApiResponse<com.woorido.post.dto.response.FileUploadResponse` | `PostController.uploadFile` | `backend/src/main/java/com/woorido/post/controller/PostController.java:431` |
| DELETE | `/challenges/{challengeId}/posts/{postId}` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  |  | `ApiResponse<com.woorido.post.dto.response.DeletePostResponse` | `PostController.deletePost` | `backend/src/main/java/com/woorido/post/controller/PostController.java:348` |
| GET | `/challenges/{challengeId}/posts/{postId}` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  |  | `ApiResponse<PostDetailResponse` | `PostController.getPostDetail` | `backend/src/main/java/com/woorido/post/controller/PostController.java:106` |
| PUT | `/challenges/{challengeId}/posts/{postId}` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  | UpdatePostRequest | `ApiResponse<CreatePostResponse` | `PostController.updatePost` | `backend/src/main/java/com/woorido/post/controller/PostController.java:182` |
| GET | `/challenges/{challengeId}/posts/{postId}/comments` | Bearer Authorization | challengeId, postId | page, size |  | `ApiResponse<List<CommentResponse` | `CommentController.getComments` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:65` |
| POST | `/challenges/{challengeId}/posts/{postId}/comments` | Bearer Authorization | challengeId, postId |  | CreateCommentRequest | `ApiResponse<Map<String, String` | `CommentController.createComment` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:40` |
| DELETE | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}` | Bearer Authorization | challengeId, commentId, postId |  |  | `ApiResponse<Void` | `CommentController.deleteComment` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:110` |
| PUT | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}` | Bearer Authorization | challengeId, commentId, postId |  | UpdateCommentRequest | `ApiResponse<UpdateCommentResponse` | `CommentController.updateComment` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:128` |
| POST | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}/like` | Bearer Authorization | challengeId, commentId, postId |  |  | `ApiResponse<Map<String, Boolean` | `CommentController.toggleLike` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:84` |
| DELETE | `/challenges/{challengeId}/posts/{postId}/like` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  |  | `ApiResponse<com.woorido.post.dto.response.PostLikeResponse` | `PostController.unlikePost` | `backend/src/main/java/com/woorido/post/controller/PostController.java:307` |
| POST | `/challenges/{challengeId}/posts/{postId}/like` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  |  | `ApiResponse<com.woorido.post.dto.response.PostLikeResponse` | `PostController.toggleLike` | `backend/src/main/java/com/woorido/post/controller/PostController.java:263` |
| PUT | `/challenges/{challengeId}/posts/{postId}/pin` | Authorization header(optional in annotation; may be validated in service) | challengeId, postId |  | PinPostRequest | `ApiResponse<PinPostResponse` | `PostController.setPostPinned` | `backend/src/main/java/com/woorido/post/controller/PostController.java:220` |

### system (4)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| POST | `/refunds` | Bearer Authorization |  |  | RefundRequest | `ApiResponse<Map<String, Object` | `SystemP1Controller.requestRefund` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:49` |
| POST | `/reports` | Bearer Authorization |  |  | CreateReportRequest | `ApiResponse<Map<String, Object` | `SystemP1Controller.createReport` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:29` |
| GET | `/search` | Bearer Authorization |  | page, q, size |  | `ApiResponse<Object` | `SystemP1Controller.search` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:75` |
| GET | `/search/challenges` | Bearer Authorization |  | page, q, size |  | `ApiResponse<Object` | `SystemP1Controller.searchChallenges` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:91` |

### user (7)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/users/check-nickname` | Public/No header |  | nickname |  | `ApiResponse<NicknameCheckResponse` | `UserController.checkNickname` | `backend/src/main/java/com/woorido/user/controller/UserController.java:121` |
| DELETE | `/users/me` | Authorization header(optional in annotation; may be validated in service) |  |  | com.woorido.user.dto.request.UserWithdrawRequest | `ApiResponse<UserWithdrawResponse` | `UserController.withdraw` | `backend/src/main/java/com/woorido/user/controller/UserController.java:95` |
| GET | `/users/me` | Authorization header(optional in annotation; may be validated in service) |  |  |  | `ApiResponse<UserProfileResponse` | `UserController.getMyProfile` | `backend/src/main/java/com/woorido/user/controller/UserController.java:44` |
| PUT | `/users/me` | Authorization header(optional in annotation; may be validated in service) |  |  | UserUpdateRequest | `ApiResponse<UserUpdateResponse` | `UserController.updateMyProfile` | `backend/src/main/java/com/woorido/user/controller/UserController.java:56` |
| PUT | `/users/me/password` | Authorization header(optional in annotation; may be validated in service) |  |  | UserPasswordChangeRequest | `ApiResponse<UserPasswordChangeResponse` | `UserController.changePassword` | `backend/src/main/java/com/woorido/user/controller/UserController.java:82` |
| PUT | `/users/me/social-onboarding` | Authorization header(optional in annotation; may be validated in service) |  |  | SocialOnboardingRequest | `ApiResponse<SocialOnboardingCompleteResponse` | `UserController.completeSocialOnboarding` | `backend/src/main/java/com/woorido/user/controller/UserController.java:69` |
| GET | `/users/{userId}` | Authorization header(optional in annotation; may be validated in service) | userId |  |  | `ApiResponse<UserPublicProfileResponse` | `UserController.getUserProfile` | `backend/src/main/java/com/woorido/user/controller/UserController.java:108` |

### vote (5)

| Method | Path | Auth | Path Params | Query Params | Body Type | Response Type | Controller.Method | Source |
|---|---|---|---|---|---|---|---|---|
| GET | `/challenges/{challengeId}/votes` | Bearer Authorization | challengeId | page, size, status, type |  | `ApiResponse<VoteListResponse` | `VoteController.getVoteList` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:34` |
| POST | `/challenges/{challengeId}/votes` | Bearer Authorization | challengeId |  | CreateVoteRequest | `ApiResponse<VoteDto` | `VoteController.createVote` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:66` |
| GET | `/votes/{voteId}` | Bearer Authorization | voteId |  |  | `ApiResponse<Object` | `VoteController.getVoteDetail` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:52` |
| PUT | `/votes/{voteId}/cast` | Bearer Authorization | voteId |  | CastVoteRequest | `ApiResponse<CastVoteResponse` | `VoteController.castVote` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:81` |
| GET | `/votes/{voteId}/result` | Bearer Authorization | voteId |  |  | `ApiResponse<VoteResultResponse` | `VoteController.getVoteResult` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:96` |

## Internal API Table

| Method | Path | Auth | Body Type | Response Type | Source |
|---|---|---|---|---|---|
| POST | `/internal/brix/calculate` | X-Api-Key | BrixMetricsBatchRequest | `BrixBatchResponse` | `backend/django/brix/views.py:61` |
| POST | `/internal/brix/ledger/chart` | X-Api-Key | LedgerGraphRequest | `LedgerGraphResponse` | `backend/django/brix/views.py:141` |
| POST | `/internal/django/brix/recalculate` | X-Internal-Api-Key |  | `ApiResponse<BrixBatchResult` | `backend/src/main/java/com/woorido/django/brix/controller/BrixInternalController.java:38` |
| GET | `/internal/runtime/info` | X-Internal-Api-Key |  | `ApiResponse<RuntimeInfoResponse` | `backend/src/main/java/com/woorido/common/controller/InternalRuntimeController.java:49` |

## Notes

- This is implementation-based inventory, not planning-only inventory.
- Some routes may be policy-blocked (e.g., write disabled) while route mapping still exists.
