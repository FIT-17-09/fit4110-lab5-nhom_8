# Readiness Checklist - Lab 05

Tick cac muc sau sau khi da chay `docker compose up -d --build --wait` va `npm run test:compose`.

- [x] **Database ready:** container DB chay healthy va `docker compose exec -T db pg_isready -U lab05` tra `accepting connections`.
- [x] **AI service ready:** AI service tra `200` cho `/health` va `/predict` hoat dong.
- [x] **API ready:** API tra `200` cho `/health`, tao/lay readings thanh cong khi token hop le.
- [x] **Environment variables:** `.env` duoc tao tu `.env.example`; khong commit secret that.
- [x] **Network & Ports:** network `team-internal` hoat dong; API goi AI qua hostname `ai-service`; ports 8000 va 9000 duoc map dung.
- [x] **Image tags:** image da duoc build/tag/push theo dang `v0.1.0-<team>` len GHCR hoac Docker Hub.

Ghi chu:

```text
- Compose stack da chay healthy voi 3 container: api, ai-service, db.
- Newman pass 19/19 assertions va sinh report trong reports/.
- Evidence screenshots da luu trong reports/screenshots/.
```
