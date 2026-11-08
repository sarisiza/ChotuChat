---
Date: 2026-11-08
tags:
  - app
  - mvp
  - claude-gen
---
# ChotuChat MVP

>[!important] Goal
>the smallest app someone could use as their daily Mastodon client — **log in, read, react, post.**

API docs: [https://docs.joinmastodon.org/client/intro/](https://docs.joinmastodon.org/client/intro/)
## MVP (v0.1)

1. **Pick a server + sign in**
    - User types an instance domain; validate and show basic info with `GET /api/v2/instance`
    - OAuth flow: `POST /api/v1/apps` → `/oauth/authorize` (Custom Tab) → `POST /oauth/token`
    - Single account only
2. **Home timeline**
    - `GET /api/v1/timelines/home`
    - Infinite scroll + pull-to-refresh
3. **Local timeline**
    - `GET /api/v1/timelines/public?local=true`
4. **Status detail / thread**
    - `GET /api/v1/statuses/:id/context`
5. **Interactions**
    - Favourite: `POST /api/v1/statuses/:id/favourite`
    - Boost: `POST /api/v1/statuses/:id/reblog`
    - Reply: `POST /api/v1/statuses` with `in_reply_to_id`
6. **Compose**
    - Text posts, character counter
    - Visibility: public / unlisted / followers / direct
    - Content warning (`spoiler_text`)
7. **Notifications**
    - `GET /api/v1/notifications` (polled, no push yet)
8. **Profiles**
    - View account + its posts: `GET /api/v1/accounts/:id`, `GET /api/v1/accounts/:id/statuses`
    - Follow / unfollow: `POST /api/v1/accounts/:id/follow`, `/unfollow`
    - Relationship state: `GET /api/v1/accounts/relationships`
9. **Own profile + logout**
    - `GET /api/v1/accounts/verify_credentials`

---

## Roadmap after MVP

### v0.2

- Post media with alt text
- Display images; blur sensitive media
- Search: `GET /api/v2/search`
- Favourites list
- Followers / following lists

### v0.3

- Push notifications (Web Push — complex on Android)
- Polls
- Lists
- Hashtags / Explore

### Later

- Sign up
- Multiple accounts
- Scheduled posts
- Filters
- Profile edit
- DMs as a conversation view

---

## Technical notes

- **Redirect URI:** instead of `urn:ietf:wg:oauth:2.0:oob` (copy/paste code), register a custom scheme like `chotuchat://oauth` and catch it with an intent filter. Use PKCE if the server supports it.
- **Pagination:** timelines page via the `Link` response header (`max_id` / `min_id`), not the JSON body. Paging 3 with a custom `PagingSource` that parses the header.
- **Post content is HTML:** convert to styled text for Compose; handle links, mentions, hashtags and custom emoji.
- **Content warnings & sensitive media:** support from day one.
- **Errors:**
    - 401 → token expired/revoked → back to login
    - 429 → rate limited → back off
- **Token storage:** encrypted DataStore, not plain SharedPreferences.
- **Stack:** Kotlin, Jetpack Compose, Retrofit or Ktor + kotlinx.serialization, Paging 3, Coil.