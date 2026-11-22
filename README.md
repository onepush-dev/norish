# Norish on Railway

[Norish](https://github.com/norish-recipes/norish) (AGPL-3.0): a realtime, family-friendly recipe app. Import recipes from websites, YouTube, Instagram or photos, plan meals on a calendar and share a synced grocery list. Deploy it on Railway with one click.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/CODE)

## What this template runs (all official images, unmodified)
- **norish**: `norishapp/norish:v0.27.0-beta`, public on port 3000, volume `/app/uploads`, health check `/api/v1/health/live`.
- **postgres**: `postgres:17-alpine`, volume, private network only.
- **valkey**: `valkey/valkey:9-alpine` with a generated password and append-only persistence (realtime events), private network only.
- **obscura**: `norishapp/obscura:0.2.7-norish.1`, the headless browser Norish uses to render recipe pages for URL import, private network only, protected by a generated CDP token.

## Variables
| Service | Variable | Value |
|---|---|---|
| norish | `AUTH_URL` | `https://${{RAILWAY_PUBLIC_DOMAIN}}` |
| norish | `DATABASE_URL` | built from the postgres service references |
| norish | `MASTER_KEY` | generated, base64 of 32 bytes (`${{secret(43)}}=`) |
| norish | `VALKEY_URL` | built from the valkey service references |
| norish | `OBSCURA_ENDPOINT`, `OBSCURA_CDP_TOKEN` | private obscura address and shared generated token |
| postgres | `POSTGRES_PASSWORD` | generated secret |
| valkey | `VALKEY_PASSWORD` | generated secret |
| obscura | `OBSCURA_CDP_TOKEN` | same generated token |

Password sign-in is on by default: the first account you register becomes the admin. Add AI, OIDC, GitHub or Google settings under Settings => Admin.

Not affiliated with Norish.
