# Output 12 - Operations Runbook (Backend + Django + Frontend)

- Generated: 2026-02-24 15:40:56

## 1) Required Runtime

- Java 21
- Node.js for frontend build/dev
- Python 3.11+ for Django 5.0.1
- Oracle connectivity for Spring datasource

## 2) Key Configuration

Spring (`backend/src/main/resources/application.properties`):
- `DJANGO_BRIX_BASE_URL` (default `http://127.0.0.1:8000`)
- `DJANGO_INTERNAL_API_KEY`
- `DJANGO_LEDGER_BASE_URL`
- `DJANGO_LEDGER_API_KEY`
- `BRIX_BATCH_INTERNAL_API_KEY`
- `brix.batch.cron=0 0 3 1 * *`
- `brix.batch.zone=Asia/Seoul`

Django (`backend/django/woorido_brix/settings.py`):
- `DJANGO_INTERNAL_API_KEY`
- `TIME_ZONE=Asia/Seoul`

## 3) Startup Order

1. Django
```bash
cd backend/django
python manage.py runserver 0.0.0.0:8000
```

2. Spring
```bash
cd backend
./gradlew.bat bootRun
```

3. Frontend
```bash
cd frontend
npm run dev
```

## 4) Health Checks

- Django ledger endpoint direct call
- Spring ledger graph endpoint via bearer token
- BRIX manual recalc endpoint via internal key

## 5) Incident Playbook

### Case A: Ledger graph fails with `LEDGER_004` / 503

Check:
1. Django process up
2. `DJANGO_LEDGER_BASE_URL` reachable from Spring runtime
3. API key match (`DJANGO_LEDGER_API_KEY` == Django `DJANGO_INTERNAL_API_KEY`)
4. direct curl to django endpoint returns 200

### Case B: Internal recalc endpoint returns 401

Check:
- request header `X-Internal-Api-Key`
- `BRIX_BATCH_INTERNAL_API_KEY` value

### Case C: Expense vote cast denied with `VOTE_007`

Check:
- meeting is `COMPLETED`
- user row in `meeting_vote_records` has `actual_attendance='ATTENDED'`

## 6) Security Note

`SecurityConfig` currently permits all requests at filter level.
Authorization is enforced mostly in controller/service logic.
For production, consider strict matcher rules in security config.
