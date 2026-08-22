# Hermex V2

**Experimental** native Kotlin/Compose client for the [Hermes Agent](https://hermes-agent.nousresearch.com/),
built as a **separate repo from the production `gravol/hermex-android`** so the look-and-feel work
doesn't touch the shipping app.

> ⚠️ **Experiment / WIP.** This is a working line for porting **Hermes WebUI's** look and feel into
> a native Android client, not a production release. API/behavior may change without notice.

## What's different vs. HermexAndroid

V2 keeps the same fundamentals as the production app — same gateway JSON-RPC/WebSocket backend
(the Hermes Dashboard on port `9119`), same notification/cron layer — but uses a **distinct app id
(`com.hermex.android.v2`) so it installs *alongside* the production app** (they can coexist and be
compared; `applicationId` differs, Kotlin package/`namespace` stays `com.hermex.android`).

- **3-bars hamburger in the chat top bar** → opens a slide-over drawer with the session list +
  menus (New session, Cron, Skills, Config, Settings) *inside* the conversation, so you never
  leave the chat to navigate. (Phase 1 — implemented.)
- WebUI-style composer chrome + token **context ring**, and WebUI-matched message/thinking/tool
  styling. (Planned — Phase 2.)

All of it runs on the same in-process agent/backend you already use; no new server, no new protocol.

## Build

```bash
./gradlew assembleRelease --no-configuration-cache
# APK: app/build/outputs/apk/release/app-release.apk
```

Same app id as HermexAndroid — **installs over/replaces** it, not side-by-side.

## Connection

Hermes Dashboard at `http://100.80.204.66:9119` (Tailscale). Login uses the dashboard
username/password; chat streams over the `ws://100.80.204.66:9119/api/ws` JSON-RPC WebSocket.
