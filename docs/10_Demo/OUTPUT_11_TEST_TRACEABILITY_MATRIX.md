# Output 11 - Test Traceability Matrix

- Generated: 2026-02-24 15:40:56
- Basis: implementation code + current automated tests

| ID | Requirement | API | Evidence | Automated Test | Manual Check |
|---:|---|---|---|---|---|
| T01 | Signup creates initial BRIX score (12.0) | `POST /auth/signup` | `SignupService.java:97`, `UserMapper.xml:246` | No | verify `user_scores.total_score=12.0` |
| T02 | `/users/me` reads BRIX from DB with 12.0 fallback | `GET /users/me` | `UserService.java:87`, `UserService.java:100` | No | compare row exists vs null |
| T03 | public profile BRIX uses same rule | `GET /users/{id}` | `UserService.java:315`, `UserService.java:320` | No | compare with `/users/me` |
| T04 | meeting attendance choice whitelist | `POST /meetings/{id}/attendance` | `MeetingService.java:670` | No | invalid choice should fail |
| T05 | complete meeting requires actualAttendees | `POST /meetings/{id}/complete` | `MeetingService.java:408` | No | null/empty should fail |
| T06 | only AGREE members can become ATTENDED | `POST /meetings/{id}/complete` | `MeetingService.java:433` | No | include non-AGREE should fail |
| T07 | expense vote eligible count uses ACTUAL attendees | `POST /challenges/{id}/votes` | `VoteService.java:564`, `MeetingMapper.xml:141` | No | no ATTENDED => fail |
| T08 | expense vote cast allowed only for ACTUAL attendee | `PUT /votes/{id}/cast` | `VoteService.java:463` | No | non-attendee => `VOTE_007` |
| T09 | kick vote quorum = 70% | vote create/cast | `VoteService.java:582` | No | verify requiredCount |
| T10 | leader kick quorum = 50% | vote create/cast | `VoteService.java:585` | No | verify requiredCount |
| T11 | leader kick allowed only after inactivity window | vote create | `VoteService.java:678` | No | recent activity should block |
| T12 | approved expense issues barcode | vote cast | `VoteService.java:724`, `VoteService.java:736` | No | barcode row created |
| T13 | manual ledger create blocked | `POST /challenges/{id}/ledger` | `LedgerService.java:75` | No | expect `LEDGER_003` |
| T14 | manual ledger update blocked | `PUT /ledger/{id}` | `LedgerService.java:88` | No | expect `LEDGER_003` |
| T15 | ledger graph delegated to django service | `GET /challenges/{id}/account/graph` | `ChallengeService.java:694`, `DjangoLedgerClient.java:53` | No | payload/response shape |
| T16 | django outage returns `LEDGER_004` 503 | same | `DjangoLedgerClient.java:64`, `GlobalExceptionHandler.java:124` | Partial | stop django and verify 503 |
| T17 | error-code-to-http mapping | all APIs | `GlobalExceptionHandler.java` | Yes | `GlobalExceptionHandlerTest` |
| T18 | internal runtime endpoint key guard | `GET /internal/runtime/info` | `InternalRuntimeController.java` | Yes | `InternalRuntimeControllerTest` |

## Current Automated Test Coverage

- Backend tests currently detected: 11 test methods
- Domain-heavy flows (meeting/vote/ledger/brix) still need service/integration tests
