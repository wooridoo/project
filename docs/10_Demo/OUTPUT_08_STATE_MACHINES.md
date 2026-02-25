# Output 08 - State Machines (Domain Lifecycle)

- Generated: 2026-02-24 15:40:56
- Source: service logic + enums in backend domain models

## 1) Challenge Status

```mermaid
stateDiagram-v2
  [*] --> RECRUITING: create challenge
  RECRUITING --> IN_PROGRESS: business start condition
  RECRUITING --> COMPLETED: deleted before start (soft-close)
  IN_PROGRESS --> DISSOLVED: dissolve vote approved
  DISSOLVED --> COMPLETED: finalization
```

Evidence:
- `backend/src/main/java/com/woorido/challenge/domain/ChallengeStatus.java`
- `backend/src/main/java/com/woorido/challenge/service/ChallengeService.java`

## 2) Meeting Status

```mermaid
stateDiagram-v2
  [*] --> SCHEDULED: create meeting
  SCHEDULED --> COMPLETED: leader completes meeting
  SCHEDULED --> CANCELLED: leader deletes/cancels meeting
```

Evidence:
- `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:183`
- `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:388`
- `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:483`

## 3) Meeting Vote Record (Attendance Response)

```mermaid
stateDiagram-v2
  [*] --> PENDING
  PENDING --> AGREE: respond attendance
  PENDING --> DISAGREE: respond attendance
  AGREE --> PENDING: cancel attendance
  DISAGREE --> PENDING: cancel attendance
  AGREE --> ATTENDED: selected in completeMeeting(actualAttendees)
```

Evidence:
- `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:319`
- `backend/src/main/java/com/woorido/meeting/service/MeetingService.java:388`

## 4) Vote Status

```mermaid
stateDiagram-v2
  [*] --> PENDING
  PENDING --> APPROVED: agree >= required
  PENDING --> REJECTED: disagree > eligible-required
  PENDING --> EXPIRED: deadline reached
```

Evidence:
- `backend/src/main/java/com/woorido/vote/service/VoteService.java:900`
- `backend/src/main/java/com/woorido/vote/service/VoteService.java:824`

## 5) Expense Request and Payment Barcode

```mermaid
stateDiagram-v2
  [*] --> VOTING
  VOTING --> APPROVED: expense vote approved
  VOTING --> REJECTED: expense vote rejected/expired
  APPROVED --> USED: barcode consumed (external/payment flow)
  APPROVED --> EXPIRED: barcode timeout
  APPROVED --> CANCELLED: manual/system cancel
```

```mermaid
stateDiagram-v2
  [*] --> ACTIVE: barcode issued
  ACTIVE --> USED: paid
  ACTIVE --> EXPIRED: timeout
  ACTIVE --> CANCELLED: cancelled
```

Evidence:
- `backend/src/main/java/com/woorido/vote/service/VoteService.java:724`
- `backend/src/main/java/com/woorido/vote/service/VoteService.java:736`
- `backend/src/main/java/com/woorido/expense/domain/ExpenseRequestStatus.java`
- `backend/src/main/java/com/woorido/expense/domain/PaymentBarcodeStatus.java`

## 6) Challenge Member Privilege

```mermaid
stateDiagram-v2
  [*] --> ACTIVE
  ACTIVE --> REVOKED: support policy violation
  ACTIVE --> LEFT: leave/kick/withdraw
  REVOKED --> ACTIVE: policy recovery
```

Evidence:
- `backend/src/main/java/com/woorido/challenge/service/ChallengeService.java`
- `backend/src/main/resources/mapper/challenge/ChallengeMemberMapper.xml`
