# Output 10 - API Examples and Postman Collection

- Generated: 2026-02-24 15:40:56
- Collection file: `Deliverables/OUTPUT_10_POSTMAN_COLLECTION.json`
- Request count: **88**
  - Spring APIs: **86**
  - Django internal APIs: **2**

## Import Steps

1. Open Postman and import `Deliverables/OUTPUT_10_POSTMAN_COLLECTION.json`.
2. Set collection variables:
- `baseUrl`: `http://localhost:8080`
- `djangoBaseUrl`: `http://localhost:8000`
- `accessToken`: valid JWT access token
- `internalApiKey`: internal API key

## Quick Smoke Order

1. `POST /auth/login`
2. `GET /users/me`
3. `GET /challenges/{challengeId}`
4. `GET /challenges/{challengeId}/account`
5. `GET /challenges/{challengeId}/account/graph?months=6`

## Key Error Cases

- `401 AUTH_*`: missing/invalid token or internal key
- `403 VOTE_007`: expense vote attempted by non-attendee
- `503 LEDGER_004`: django ledger service unavailable
