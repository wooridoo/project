# Output 05 - Additional Deliverables

- Generated: 2026-02-24

## A. Doc-Code consistency check

| Item | Doc value | Runtime/Code value | Finding |
|---|---:|---:|---|
| DB table count | 32 (document header) | 33 (actual section count) | Header count differs from section-defined table count |
| API endpoint count | 92 in API_SPECIFICATION_1.0.0 | 86 Spring (84 external + 2 internal) + 2 Django internal | Planning spec and implemented routes are not 1:1 |
| FK relation count | 56 in DB document footer | 58 FK bullets reflected in Output 01/02 | Footer summary and section-level definitions are not fully aligned |

## B. Mapper -> Table traceability matrix

| Mapper XML | Referenced tables |
|---|---|
| `backend/src/main/resources/mapper/account/AccountMapper.xml` | `account_transactions`, `accounts` |
| `backend/src/main/resources/mapper/account/SessionMapper.xml` | `sessions` |
| `backend/src/main/resources/mapper/challenge/ChallengeMapper.xml` | `challenge_members`, `challenges`, `ledger_entries`, `users` |
| `backend/src/main/resources/mapper/challenge/ChallengeMemberMapper.xml` | `challenge_members`, `user_scores`, `users` |
| `backend/src/main/resources/mapper/challenge/LedgerEntryMapper.xml` | `ledger_entries` |
| `backend/src/main/resources/mapper/challenge/LedgerMapper.xml` | `ledger_entries` |
| `backend/src/main/resources/mapper/django/BrixMetricMapper.xml` | `account_transactions`, `accounts`, `comment_likes`, `comments`, `general_votes`, `meeting_vote_records`, `meeting_votes`, `meetings`, `post_likes`, `posts`, `users` |
| `backend/src/main/resources/mapper/expense/ExpenseRequestMapper.xml` | `expense_requests`, `expense_votes`, `meetings` |
| `backend/src/main/resources/mapper/expense/PaymentBarcodeMapper.xml` | `payment_barcodes` |
| `backend/src/main/resources/mapper/meeting/MeetingMapper.xml` | `challenge_members`, `meeting_vote_records`, `meeting_votes`, `meetings`, `users` |
| `backend/src/main/resources/mapper/meeting/MeetingVoteMapper.xml` | `meeting_vote_records`, `meeting_votes` |
| `backend/src/main/resources/mapper/notification/NotificationMapper.xml` | `notification_settings`, `notifications` |
| `backend/src/main/resources/mapper/post/CommentLikeMapper.xml` | `comment_likes` |
| `backend/src/main/resources/mapper/post/CommentMapper.xml` | `comments`, `users` |
| `backend/src/main/resources/mapper/post/PostImageMapper.xml` | `post_images` |
| `backend/src/main/resources/mapper/post/PostLikeMapper.xml` | `post_likes` |
| `backend/src/main/resources/mapper/post/PostMapper.xml` | `post_images`, `post_likes`, `posts`, `users` |
| `backend/src/main/resources/mapper/UserMapper.xml` | `account_transactions`, `accounts`, `challenge_members`, `challenges`, `user_scores`, `users` |
| `backend/src/main/resources/mapper/vote/ExpenseVoteMapper.xml` | `expense_vote_records`, `expense_votes` |
| `backend/src/main/resources/mapper/vote/GeneralVoteMapper.xml` | `general_vote_records`, `general_votes` |
| `backend/src/main/resources/mapper/vote/VoteMapper.xml` | `meeting_vote_records`, `meeting_votes`, `meetings`, `users` |
| `backend/src/main/resources/mapper/vote/VoteQueryMapper.xml` | `challenge_members`, `expense_requests`, `expense_vote_records`, `expense_votes`, `general_vote_records`, `general_votes`, `meeting_vote_records`, `meeting_votes`, `meetings`, `users` |

## C. Table coverage from mapper perspective

- In mapper but not in DB_Schema_1.0.0: None
- In DB_Schema_1.0.0 but not referenced in mapper XML: admin_logs, admins, fee_policies, payment_logs, refresh_tokens, refunds, reports, settlements, webhook_logs

## D. Operational checklist artifact

| Checkpoint | Expected | How to verify |
|---|---|---|
| Django ledger connectivity | `/challenges/{id}/account/graph` returns 200 | Validate Django 8000 port and `django.ledger.base-url` |
| BRIX internal trigger | `/internal/django/brix/recalculate` returns 200 | Validate `X-Internal-Api-Key` and Django API key |
| Ledger consistency | monthly balances are cumulative and monotonic by ledger events | Compare SQL month-end balance vs graph payload |
| Vote eligibility | only COMPLETED + ATTENDED members can vote expense | Re-run service tests and API smoke tests |
| UTF-8 safety | no mojibake in API error messages | Validate response payload and frontend rendering |

## E. Follow-up artifacts status

- Implemented: `OUTPUT_09_SEQUENCE_DIAGRAMS.md`
- Implemented: `OUTPUT_10_API_EXAMPLES_POSTMAN.md`
- Implemented: `OUTPUT_10_POSTMAN_COLLECTION.json`
- Implemented: `OUTPUT_11_TEST_TRACEABILITY_MATRIX.md`
- Implemented: `OUTPUT_12_OPERATIONS_RUNBOOK.md`
- Implemented: `OUTPUT_13_DEMO_SCENARIOS.md`
