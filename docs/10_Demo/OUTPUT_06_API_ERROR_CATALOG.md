# Output 06 - API Error Catalog (Code-Based)

- Generated: 2026-02-24 15:40:56
- Source: backend exception throw sites + GlobalExceptionHandler status mapping

## Summary
- Total unique error codes: **89**
- Prefix groups: **18**
- Mapping authority: `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java`

## Prefix Counts

| Prefix | Count |
|---|---:|
| `ABUSE` | 1 |
| `ACCOUNT` | 14 |
| `AUTH` | 14 |
| `BRIX` | 1 |
| `CHALLENGE` | 10 |
| `COMMENT` | 4 |
| `FILE` | 1 |
| `IMAGE` | 4 |
| `LEDGER` | 4 |
| `MEETING` | 6 |
| `MEMBER` | 2 |
| `NOTIFICATION` | 3 |
| `POST` | 5 |
| `SEARCH` | 1 |
| `SUPPORT` | 1 |
| `USER` | 7 |
| `VALIDATION` | 1 |
| `VOTE` | 10 |

## Code Table

| Code | HTTP | Occurrences | Prefix | First Seen |
|---|---:|---:|---|---|
| `ABUSE_001` | 500 | 4 | `ABUSE` | `backend/src/main/java/com/woorido/post/service/SocialRateLimitService.java:27` |
| `ACCOUNT_001` | 404 | 9 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:77` |
| `ACCOUNT_002` | 400 | 2 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:210` |
| `ACCOUNT_003` | 400 | 3 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/strategy/DefaultWithdrawalPolicy.java:16` |
| `ACCOUNT_004` | 400 | 3 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:431` |
| `ACCOUNT_005` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/strategy/DefaultWithdrawalPolicy.java:20` |
| `ACCOUNT_006` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/strategy/DefaultWithdrawalPolicy.java:24` |
| `ACCOUNT_007` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:213` |
| `ACCOUNT_008` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:217` |
| `ACCOUNT_009` | 400 | 2 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:262` |
| `ACCOUNT_010` | 409 | 3 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:275` |
| `ACCOUNT_011` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:266` |
| `ACCOUNT_012` | 400 | 1 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:277` |
| `ACCOUNT_013` | 400 | 2 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:282` |
| `ACCOUNT_014` | 400 | 4 | `ACCOUNT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:304` |
| `AUTH_001` | 401 | 33 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:79` |
| `AUTH_002` | 401 | 3 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:79` |
| `AUTH_004` | 401 | 3 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:246` |
| `AUTH_007` | 401 | 3 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:218` |
| `AUTH_009` | 401 | 3 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:282` |
| `AUTH_010` | 401 | 2 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:265` |
| `AUTH_011` | 401 | 5 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:115` |
| `AUTH_012` | 401 | 6 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:118` |
| `AUTH_013` | 401 | 8 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:118` |
| `AUTH_014` | 401 | 5 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:146` |
| `AUTH_015` | 401 | 2 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:149` |
| `AUTH_016` | 401 | 2 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:150` |
| `AUTH_017` | 401 | 2 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:147` |
| `AUTH_018` | 401 | 5 | `AUTH` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:148` |
| `BRIX_001` | 400 | 5 | `BRIX` | `backend/src/main/java/com/woorido/django/brix/client/DjangoBrixClient.java:41` |
| `CHALLENGE_001` | 404 | 27 | `CHALLENGE` | `backend/src/main/java/com/woorido/account/service/AccountService.java:416` |
| `CHALLENGE_002` | 400 | 3 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:199` |
| `CHALLENGE_003` | 403 | 20 | `CHALLENGE` | `backend/src/main/java/com/woorido/account/service/AccountService.java:421` |
| `CHALLENGE_004` | 403 | 9 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:238` |
| `CHALLENGE_005` | 400 | 4 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:201` |
| `CHALLENGE_006` | 400 | 2 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:203` |
| `CHALLENGE_007` | 400 | 2 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:275` |
| `CHALLENGE_010` | 400 | 2 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:369` |
| `CHALLENGE_011` | 409 | 5 | `CHALLENGE` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:241` |
| `CHALLENGE_014` | 400 | 4 | `CHALLENGE` | `backend/src/main/java/com/woorido/account/service/AccountService.java:453` |
| `COMMENT_002` | 404 | 7 | `COMMENT` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:22` |
| `COMMENT_003` | 403 | 4 | `COMMENT` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:34` |
| `COMMENT_004` | 400 | 2 | `COMMENT` | `backend/src/main/java/com/woorido/post/service/CommentService.java:99` |
| `COMMENT_005` | 400 | 1 | `COMMENT` | `backend/src/main/java/com/woorido/post/service/CommentService.java:369` |
| `FILE_001` | 400 | 1 | `FILE` | `backend/src/main/java/com/woorido/common/strategy/LocalImageUploadStrategy.java:51` |
| `IMAGE_001` | 400 | 3 | `IMAGE` | `backend/src/main/java/com/woorido/common/image/ImagePolicyValidator.java:40` |
| `IMAGE_002` | 400 | 3 | `IMAGE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:70` |
| `IMAGE_003` | 400 | 4 | `IMAGE` | `backend/src/main/java/com/woorido/common/image/ImagePolicyValidator.java:69` |
| `IMAGE_004` | 400 | 4 | `IMAGE` | `backend/src/main/java/com/woorido/common/image/ImagePolicyValidator.java:24` |
| `LEDGER_001` | 404 | 5 | `LEDGER` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:92` |
| `LEDGER_002` | 400 | 1 | `LEDGER` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:96` |
| `LEDGER_003` | 400 | 3 | `LEDGER` | `backend/src/main/java/com/woorido/challenge/controller/LedgerController.java:89` |
| `LEDGER_004` | 503 | 3 | `LEDGER` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:171` |
| `MEETING_001` | 404 | 13 | `MEETING` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:24` |
| `MEETING_002` | 400 | 3 | `MEETING` | `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:270` |
| `MEETING_003` | 400 | 7 | `MEETING` | `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:410` |
| `MEETING_004` | 400 | 1 | `MEETING` | `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:193` |
| `MEETING_005` | 400 | 2 | `MEETING` | `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:402` |
| `MEETING_006` | 400 | 3 | `MEETING` | `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:335` |
| `MEMBER_001` | 403 | 22 | `MEMBER` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:431` |
| `MEMBER_002` | 403 | 3 | `MEMBER` | `backend/src/main/java/com/woorido/challenge/controller/ChallengeController.java:313` |
| `NOTIFICATION_001` | 400 | 4 | `NOTIFICATION` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:166` |
| `NOTIFICATION_002` | 403 | 4 | `NOTIFICATION` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:38` |
| `NOTIFICATION_003` | 400 | 4 | `NOTIFICATION` | `backend/src/main/java/com/woorido/notification/controller/NotificationController.java:169` |
| `POST_001` | 404 | 17 | `POST` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:25` |
| `POST_002` | 403 | 7 | `POST` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:35` |
| `POST_004` | 403 | 5 | `POST` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:36` |
| `POST_005` | 403 | 3 | `POST` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:37` |
| `POST_007` | 400 | 2 | `POST` | `backend/src/main/java/com/woorido/common/strategy/LocalImageUploadStrategy.java:24` |
| `SEARCH_001` | 400 | 2 | `SEARCH` | `backend/src/main/java/com/woorido/system/controller/SystemP1Controller.java:85` |
| `SUPPORT_001` | 400 | 1 | `SUPPORT` | `backend/src/main/java/com/woorido/account/service/AccountService.java:426` |
| `USER_001` | 404 | 4 | `USER` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:262` |
| `USER_002` | 400 | 2 | `USER` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:99` |
| `USER_003` | 400 | 2 | `USER` | `backend/src/main/java/com/woorido/user/service/UserService.java:230` |
| `USER_005` | 400 | 4 | `USER` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:82` |
| `USER_006` | 400 | 4 | `USER` | `backend/src/main/java/com/woorido/user/dto/request/UserUpdateRequest.java:12` |
| `USER_007` | 409 | 3 | `USER` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:46` |
| `USER_009` | 400 | 1 | `USER` | `backend/src/main/java/com/woorido/user/service/UserService.java:227` |
| `VALIDATION_001` | 400 | 19 | `VALIDATION` | `backend/src/main/java/com/woorido/auth/controller/AuthController.java:282` |
| `VOTE_001` | 404 | 10 | `VOTE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:27` |
| `VOTE_002` | 400 | 2 | `VOTE` | `backend/src/main/java/com/woorido/vote/service/VoteService.java:75` |
| `VOTE_003` | 403 | 6 | `VOTE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:39` |
| `VOTE_004` | 400 | 12 | `VOTE` | `backend/src/main/java/com/woorido/vote/service/VoteService.java:72` |
| `VOTE_005` | 400 | 2 | `VOTE` | `backend/src/main/java/com/woorido/vote/service/VoteService.java:420` |
| `VOTE_006` | 409 | 6 | `VOTE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:47` |
| `VOTE_007` | 403 | 4 | `VOTE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:40` |
| `VOTE_008` | 403 | 3 | `VOTE` | `backend/src/main/java/com/woorido/common/exception/GlobalExceptionHandler.java:41` |
| `VOTE_009` | 400 | 3 | `VOTE` | `backend/src/main/java/com/woorido/vote/service/VoteService.java:94` |
| `VOTE_010` | 400 | 2 | `VOTE` | `backend/src/main/java/com/woorido/vote/service/VoteService.java:683` |

## Notes
- Responses follow `CODE:message` pattern.
- Status resolution is centralized in `GlobalExceptionHandler`.
