# OUTPUT 09 - Core Sequence Diagrams (Implementation-Based)

- Generated: 2026-02-24 15:40:56
- Source scope: backend services/controllers, django views, frontend hooks/apis
- Scanned files: **715**

## 1) Ledger Graph Read (`GET /challenges/{challengeId}/account/graph`)

```mermaid
sequenceDiagram
    autonumber
    participant FE as Frontend(useChallengeAccountGraph)
    participant CC as ChallengeController
    participant CS as ChallengeService
    participant CM as ChallengeMapper
    participant DLC as DjangoLedgerClient
    participant DJ as Django /internal/brix/ledger/chart

    FE->>CC: GET /challenges/{challengeId}/account/graph?months=6
    CC->>CS: getChallengeLedgerGraph(challengeId, token, months)
    CS->>CM: findChallengeAccount + findLedgerEntriesForGraph
    CS->>DLC: calculateGraph(request)
    DLC->>DJ: POST /internal/brix/ledger/chart + X-Api-Key
    DJ-->>DLC: monthlyExpenses + monthlyBalances
    DLC-->>CS: DjangoLedgerGraphResponse
    CS-->>CC: ChallengeLedgerGraphResponse
    CC-->>FE: 200 ApiResponse.success(data)

    alt django unavailable
        DLC-->>CS: RuntimeException(LEDGER_004)
        CC-->>FE: 503 LEDGER_004
    end
```

## 2) Complete Meeting with Actual Attendees

```mermaid
sequenceDiagram
    autonumber
    participant FE as Frontend(CompleteMeetingModal)
    participant MC as MeetingController
    participant MS as MeetingService
    participant CMM as ChallengeMemberMapper
    participant MM as MeetingMapper
    participant MVM as MeetingVoteMapper

    FE->>MC: POST /meetings/{meetingId}/complete {actualAttendees[]}
    MC->>MS: completeMeeting(meetingId, token, request)
    MS->>MS: validate actualAttendees required/non-empty/no-duplicate/no-blank
    loop each attendeeId
        MS->>CMM: verify ACTIVE challenge member
        MS->>MM: verify AGREE response (isAttendee)
        MS->>MVM: set actual_attendance='ATTENDED'
    end
    MS->>MM: set meeting status COMPLETED
    MC-->>FE: 200
```

## 3) Expense Vote Cast Eligibility

```mermaid
sequenceDiagram
    autonumber
    participant FE as Frontend(castVote)
    participant VC as VoteController
    participant VS as VoteService
    participant EM as ExpenseVoteMapper
    participant MM as MeetingMapper

    FE->>VC: PUT /votes/{voteId}/cast {choice}
    VC->>VS: castVote(voteId, userId, request)
    VS->>EM: load expenseVote + expenseRequest
    VS->>MM: isActualAttendee(meetingId, userId)
    alt not actual attendee
        VS-->>VC: VOTE_007
        VC-->>FE: 403
    else allowed
        VS->>EM: insert vote record
        VS->>VS: finalize by quorum
        VC-->>FE: 200
    end
```

## 4) BRIX Monthly Batch and Manual Trigger

```mermaid
sequenceDiagram
    autonumber
    participant SCH as BrixBatchScheduler
    participant BBS as BrixBatchService
    participant BMM as BrixMetricMapper
    participant DBC as DjangoBrixClient
    participant DJ as Django /internal/brix/calculate
    participant UM as UserMapper(user_scores)

    SCH->>BBS: runMonthlyBrixBatch()
    BBS->>BMM: findMetricsUpTo(cutoffAt)
    BBS->>DBC: POST /internal/brix/calculate
    DBC->>DJ: users metrics + X-Api-Key
    DJ-->>DBC: computed totalScore list
    DBC-->>BBS: response
    loop each user
        BBS->>UM: upsertTotalScoreByUserId
    end
```
