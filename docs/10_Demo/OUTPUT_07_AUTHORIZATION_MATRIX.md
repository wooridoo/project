# Output 07 - Authorization Matrix (Implemented API)

- Generated: 2026-02-24 15:40:56
- Source: controller mappings + auth hints from parameter annotations

## Important Context
- `SecurityConfig` currently uses `requestMatchers("/**").permitAll()`.
- Effective authorization is mostly enforced in services/controllers via token parsing and role checks.

## Endpoint Matrix

| Method | Path | Auth Hint | Access Scope | Source |
|---|---|---|---|---|
| POST | `/accounts/charge` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:67` |
| POST | `/accounts/charge/callback` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:80` |
| GET | `/accounts/me` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:113` |
| GET | `/accounts/me/transactions` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:42` |
| POST | `/accounts/support` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:104` |
| POST | `/accounts/withdraw` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/account/controller/AccountController.java:91` |
| POST | `/auth/email/confirm` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:210` |
| POST | `/auth/email/verify` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:199` |
| POST | `/auth/login` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:71` |
| POST | `/auth/logout` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:225` |
| POST | `/auth/password/reset` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:253` |
| PUT | `/auth/password/reset` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:272` |
| POST | `/auth/refresh` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:239` |
| POST | `/auth/signup` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:89` |
| GET | `/auth/social/callback/{provider}` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:161` |
| POST | `/auth/social/complete` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:132` |
| GET | `/auth/social/providers` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:126` |
| POST | `/auth/social/start` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:106` |
| GET | `/challenges` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:58` |
| POST | `/challenges` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:258` |
| GET | `/challenges/me` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:84` |
| DELETE | `/challenges/{challengeId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:351` |
| GET | `/challenges/{challengeId}` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:105` |
| PUT | `/challenges/{challengeId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:218` |
| GET | `/challenges/{challengeId}/account` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:130` |
| GET | `/challenges/{challengeId}/account/graph` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:154` |
| POST | `/challenges/{challengeId}/delegate` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:442` |
| POST | `/challenges/{challengeId}/join` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:186` |
| DELETE | `/challenges/{challengeId}/leave` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:298` |
| GET | `/challenges/{challengeId}/ledger` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:27` |
| POST | `/challenges/{challengeId}/ledger` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:55` |
| GET | `/challenges/{challengeId}/ledger/summary` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:42` |
| GET | `/challenges/{challengeId}/meetings` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:32` |
| POST | `/challenges/{challengeId}/meetings` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:57` |
| GET | `/challenges/{challengeId}/members` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:325` |
| GET | `/challenges/{challengeId}/members/{memberId}` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:412` |
| GET | `/challenges/{challengeId}/posts` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:144` |
| POST | `/challenges/{challengeId}/posts` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:63` |
| POST | `/challenges/{challengeId}/posts/images` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:381` |
| POST | `/challenges/{challengeId}/posts/upload` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:431` |
| DELETE | `/challenges/{challengeId}/posts/{postId}` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:348` |
| GET | `/challenges/{challengeId}/posts/{postId}` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:106` |
| PUT | `/challenges/{challengeId}/posts/{postId}` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:182` |
| GET | `/challenges/{challengeId}/posts/{postId}/comments` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:65` |
| POST | `/challenges/{challengeId}/posts/{postId}/comments` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:40` |
| DELETE | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:110` |
| PUT | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:128` |
| POST | `/challenges/{challengeId}/posts/{postId}/comments/{commentId}/like` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/CommentController.java:84` |
| DELETE | `/challenges/{challengeId}/posts/{postId}/like` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:307` |
| POST | `/challenges/{challengeId}/posts/{postId}/like` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:263` |
| PUT | `/challenges/{challengeId}/posts/{postId}/pin` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/post/controller/PostController.java:220` |
| PUT | `/challenges/{challengeId}/support/settings` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:381` |
| GET | `/challenges/{challengeId}/votes` | `OPTIONAL_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:34` |
| POST | `/challenges/{challengeId}/votes` | `REQUIRED_BEARER` | `CHALLENGE_MEMBER_OR_ROLE` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:66` |
| POST | `/internal/django/brix/recalculate` | `INTERNAL_API_KEY` | `INTERNAL_ONLY` | `backend/src/main/java/com/woorido/django/brix/controller/BrixInternalController.java:38` |
| GET | `/internal/runtime/info` | `INTERNAL_API_KEY` | `INTERNAL_ONLY` | `backend/src/main/java/com/woorido/common/controller/InternalRuntimeController.java:49` |
| PUT | `/ledger/{entryId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:69` |
| DELETE | `/meetings/{meetingId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:110` |
| GET | `/meetings/{meetingId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:45` |
| PUT | `/meetings/{meetingId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:71` |
| DELETE | `/meetings/{meetingId}/attendance` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:122` |
| POST | `/meetings/{meetingId}/attendance` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:84` |
| POST | `/meetings/{meetingId}/complete` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/meeting/controller/MeetingController.java:97` |
| GET | `/notifications` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:41` |
| PUT | `/notifications/read-all` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:112` |
| GET | `/notifications/settings` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:128` |
| PUT | `/notifications/settings` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:140` |
| GET | `/notifications/{notificationId}` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:77` |
| PUT | `/notifications/{notificationId}/read` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:91` |
| POST | `/refunds` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:49` |
| POST | `/reports` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:29` |
| GET | `/search` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:75` |
| GET | `/search/challenges` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:91` |
| POST | `/uploads/challenges/banner` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:28` |
| POST | `/uploads/challenges/thumbnail` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:49` |
| GET | `/users/check-nickname` | `NONE` | `PUBLIC` | `backend/src/main/java/com/woorido/user/controller/UserController.java:121` |
| DELETE | `/users/me` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/user/controller/UserController.java:95` |
| GET | `/users/me` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/user/controller/UserController.java:44` |
| PUT | `/users/me` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/user/controller/UserController.java:56` |
| PUT | `/users/me/password` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/user/controller/UserController.java:82` |
| POST | `/users/me/profile-image` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/common/controller/ImageUploadController.java:70` |
| PUT | `/users/me/social-onboarding` | `OPTIONAL_BEARER` | `AUTH_USER` | `backend/src/main/java/com/woorido/user/controller/UserController.java:69` |
| GET | `/users/{userId}` | `OPTIONAL_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/user/controller/UserController.java:108` |
| GET | `/votes/{voteId}` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:52` |
| PUT | `/votes/{voteId}/cast` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:81` |
| GET | `/votes/{voteId}/result` | `REQUIRED_BEARER` | `AUTH_USER_OR_SERVICE_GUARD` | `backend/src/main/java/com/woorido/vote/controller/VoteController.java:96` |

## Notes
- `Auth Hint` is extracted from controller signature/annotation style, not from Spring Security matcher rules.
- For production hardening, move critical authorization from runtime exceptions to security filter rules where possible.
