# Roadmap

Cross-platform social media scheduling and automation — built in public by
[@jjudkins77](https://twitter.com/jjudkins77), DjangoCon US Marketing Chair.

Follow along: [Twitter](https://twitter.com/jjudkins77) · [Mastodon](https://fosstodon.org/@jjudkins) · [LinkedIn](https://www.linkedin.com/in/jasoncjudkins/) · [Blog](https://judkins.dev/blog)

---

## Phase 1 — Foundation

- [x] Django project setup (REST Framework, Celery, Redis, JWT auth)
- [x] Data models — 14 models covering accounts, posts, scheduling, analytics
- [x] PostgreSQL configuration with Docker Compose for local dev
- [x] Encrypted OAuth token storage (Fernet, no plaintext secrets at rest)
- [x] Multi-user + team/organisation support in the data layer
- [x] Thread/reply support (Twitter threads, Mastodon chains)
- [x] Recurring schedule model
- [x] Media asset model (images, video, GIFs — S3-ready)
- [x] Django admin for all models

## Phase 2 — Platform Integrations

- [ ] Twitter/X — OAuth 2.0 connect + post text + images
- [ ] Bluesky — ATP app password connect + post text + images
- [ ] LinkedIn — OAuth 2.0 connect + post text
- [ ] Mastodon — OAuth 2.0 connect + post text + images
- [ ] Instagram — Facebook Graph API connect + post images

## Phase 3 — Scheduling Engine

- [ ] Celery task queue wired to PostTarget publishing
- [ ] Schedule a post to one or more platforms at a specific time
- [ ] Retry logic for failed publishes
- [ ] Recurring schedule execution (daily / weekly / bi-weekly / monthly)

## Phase 4 — Web Dashboard

- [ ] Authentication (login, register, JWT)
- [ ] Compose post — write once, select platforms
- [ ] Per-platform content overrides (e.g. shorter copy for Twitter)
- [ ] Media upload and attachment
- [ ] Calendar / queue view of scheduled posts
- [ ] Post history and status

## Phase 5 — Analytics

- [ ] Pull engagement metrics per post per platform
- [ ] Historical metric snapshots (likes, reposts, replies, impressions)
- [ ] Account follower growth over time
- [ ] Basic analytics dashboard

## Phase 6 — Polish & Launch

- [ ] GitHub Actions CI/CD pipeline
- [ ] AWS deployment (ECS or Elastic Beanstalk)
- [ ] Waitlist / early access sign-up
- [ ] Documentation and setup guide
- [ ] Public beta

---

> Built to solve a real problem — managing DjangoCon US social media across five platforms from one place.