# Changelog

All notable progress on this project is documented here.

Follow along: [Twitter](https://twitter.com/jjudkins77) · [Mastodon](https://fosstodon.org/@jjudkins) · [LinkedIn](https://www.linkedin.com/in/jasoncjudkins/) · [Blog](https://judkins.dev/blog)

---

## [Unreleased]

---

## 2026-02-24 — Foundation complete

### Added

**Data models (14 total across 5 files)**

The entire database layer is in place. Every major concept in the app now has a model:

- `UserProfile` — timezone, avatar, bio extending Django's built-in User
- `Organization` + `OrganizationMembership` — team workspaces with owner / admin / editor / viewer roles
- `SocialMediaAccount` — stores connected accounts for Twitter/X, Bluesky, LinkedIn, Mastodon, Instagram; OAuth tokens encrypted at rest
- `AccountMetric` — point-in-time follower count snapshots for trend tracking
- `Post` — the core content unit; supports draft → scheduled → published lifecycle, thread/reply chains, tags, and media
- `PostTarget` — one row per platform destination per post; tracks publish status, platform post ID, and retry count independently per platform
- `PostActivityLog` — immutable audit trail for every action taken on a post
- `ContentTemplate` — reusable post templates per platform
- `MediaAsset` — image/video/GIF storage with dimensions, duration, MIME type, and alt text; S3-ready
- `Tag` — user-defined labels with hex colour for the UI
- `RecurringSchedule` — daily/weekly/bi-weekly/monthly cadences tied to a template and a set of accounts
- `PostMetric` — time-series engagement snapshots (likes, reposts, replies, impressions, reach, link clicks)

**Security**

- Replaced `django-cryptography` (incompatible with Django 4+) with a custom `EncryptedTextField` using `cryptography.fernet` directly — no third-party dependency, raises `ImproperlyConfigured` in production if the key is missing so secrets are never silently stored as plain text

**PostgreSQL setup**

- `config/settings.py` updated to use `dj-database-url` — set `DATABASE_URL` in the environment to switch from SQLite to PostgreSQL with no code changes
- `docker-compose.yml` added — `docker compose up -d` starts PostgreSQL 16 and Redis 7 locally
- `.env.example` added — documents every environment variable the app reads

**Project hygiene**

- `config/settings.py` wired up: DRF with JWT auth + pagination, CORS, Celery + Redis broker/cache, S3 storage toggle, Sentry error tracking, `python-decouple` for env-based config
- `.gitignore` populated (was empty) — covers `__pycache__`, SQLite dev DB, media/static build dirs, `.env`, virtual environments, IDE files, Celery beat schedule
- Initial Django migration generated and verified (`python manage.py check` passes)
- All 14 models registered in Django admin with search, filter, and inline support

---

> Started this project to solve a real problem: managing DjangoCon US social media across five platforms from one place.