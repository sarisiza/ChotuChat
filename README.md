# ChotuChat

An Android client for [Mastodon](https://joinmastodon.org), the decentralized, open-source social network.

> **Status:** early development. We're working toward the first usable release (v0.1). Expect breaking changes.

## Why ChotuChat?

Mastodon is decentralized and open source, but there are only a handful of apps for it, and plenty of people still don't use one. ChotuChat aims to be a simple, friendly daily client for:

- **Current Mastodon users** who want another good way to use the network.
- **Newcomers** who are tired of traditional, centralized social media and want something different.

## Features

### v0.1 (MVP): log in, read, react, post

- [ ] Pick a server and sign in with OAuth (one account)
- [ ] Home timeline with infinite scroll and pull-to-refresh
- [ ] Local timeline
- [ ] Status detail and thread view
- [ ] Favourite, boost and reply
- [ ] Compose text posts with a character counter, visibility options and content warnings
- [ ] Notifications (polled)
- [ ] View profiles, follow and unfollow
- [ ] Your own profile and logout

### Roadmap

| Version | Planned |
| ------- | ------- |
| v0.2 | Media posts with alt text, image display with sensitive-media blur, search, favourites list, followers/following lists |
| v0.3 | Push notifications, polls, lists, hashtags and Explore |
| Later | Sign up, multiple accounts, scheduled posts, filters, profile edit, DM conversation view |

## Tech stack

- **Language:** Kotlin
- **UI:** Jetpack Compose
- **Networking:** Retrofit or Ktor, with kotlinx.serialization
- **Pagination:** Paging 3 (custom `PagingSource` that reads Mastodon's `Link` header)
- **Images:** Coil
- **Secure storage:** encrypted DataStore for OAuth tokens

## Getting started

### Requirements

- Android Studio (latest stable)
- JDK 17
- An Android device or emulator running Android _XX_ or later <!-- TODO: set minSdk -->

### Build and run

```bash
git clone https://github.com/sarisiza/ChotuChat.git
cd ChotuChat
./gradlew installDebug
```

Or open the project in Android Studio and press **Run**.

### Signing in

ChotuChat registers itself with your Mastodon instance the first time you log in, so you don't need API keys. Type your server's domain (for example `mastodon.social`), approve access in the browser and you'll be sent back to the app.

## How it works

- **Authentication:** `POST /api/v1/apps` → `/oauth/authorize` (opened in a Custom Tab) → `POST /oauth/token`. The redirect uses a custom scheme (`chotuchat://oauth`) caught by an intent filter, with PKCE where the server supports it.
- **Post content** comes from the server as HTML and is converted to styled text, including links, mentions, hashtags and custom emoji.
- **Errors:** a `401` sends you back to login; a `429` (rate limit) triggers a back-off.

API reference: [docs.joinmastodon.org](https://docs.joinmastodon.org/client/intro/)

## Contributing

Contributions, bug reports and ideas are welcome. Please open an issue to talk about bigger changes before you send a pull request.

<!-- TODO: add CONTRIBUTING.md and code style notes -->

## License

<!-- TODO: choose a license (e.g. GPL-3.0, Apache-2.0, MIT) -->
_TBD_
