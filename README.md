  1 # Instagram SSL Pinning Bypass — Android
      2
      3 Pre-patched Instagram APK with certificate pinning fully disabled. Intercept API calls, GraphQL queries, media streams, and auth flows using any MITM proxy.
      4
      5 **No root. No Frida. No Magisk.** The patch is baked into the APK.
      6
      7 ---
      8
      9 ## How It Works
     10
     11 Instagram uses two layers of SSL protection:
     12
     13 1. **Network Security Config** — restricts trusted CA certificates to system-only
     14 2. **Hardcoded pinning** — `CertificatePinner`, `TrustManager`, and custom verifiers in the smali code reject any certificate that doesn't match their pinned keys
     15
     16 This patch neutralizes both layers:
     17 - NSC modified to accept user-installed CA certificates with `overridePins="true"`
     18 - All pinning verification methods patched to return without checking
     19
     20 Result: your proxy's CA certificate is trusted, and HTTPS traffic is fully visible.
     21
     22 ---
     23
     24 ## What You Can Capture
     25
     26 - REST API endpoints and request/response payloads
     27 - GraphQL queries (feed, stories, DMs, search)
     28 - Media delivery URLs and CDN traffic
     29 - Authentication and session token flows
     30 - Content recommendation and ranking signals
     31 - Analytics and tracking events
     32
     33 ---
     34
     35 ## Setup
     36
     37 ### On a Physical Device
     38
     39 1. Install the patched APK
     40 2. Set your Wi-Fi proxy to your PC's IP address (port 8080)
     41 3. Install your proxy's CA certificate on the phone
     42 4. Open Instagram — traffic appears in your proxy
     43
     44 ### On an Emulator
     45
     46 1. Install the APK on Nox, LDPlayer, or BlueStacks
     47 2. Configure the emulator's proxy settings
     48 3. Install the CA certificate
     49 4. Launch Instagram
     50
     51 ### Compatible Proxy Tools
     52
     53 | Tool | Type |
     54 |---|---|
     55 | Burp Suite | Desktop, full-featured |
     56 | mitmproxy | CLI / Web UI, open source |
     57 | Reqable | Desktop, modern UI |
     58 | Proxypin | Lightweight, free |
     59
     60 ---
     61
     62 ## Supported Builds
     63
     64 | Version | Architecture | Status |
     65 |---|---|---|
     66 | 435.0.0.37.76 | arm64-v8a, x86_64 | Available — DM on Telegram |
     67 | 370.1.0.43.96 | arm64-v8a, x86_64 | Demo in Releases |
     68
     69 Newer versions patched on request.
     70
     71 ---
     72
     73 ## Other Projects
     74
     75 - [TikTok SSL Pinning Bypass](#) — TikTok traffic interception
     76 - [Snapchat SSL Pinning Bypass](#) — Snapchat API analysis
     77 - [Threads SSL Pinning Bypass](#) — Threads HTTPS capture
     78 - [Facebook SSL Pinning Bypass](#) — Facebook API traffic
     79 - [Messenger SSL Pinning Bypass](#) — Messenger protocol analysis
     80
     81 ---
     82
     83 ## Get the Latest Build
     84
     85 For the most recent patched Instagram APK or custom version requests:
     86
     87 **[Telegram](https://t.me/YOUR_USERNAME)**
