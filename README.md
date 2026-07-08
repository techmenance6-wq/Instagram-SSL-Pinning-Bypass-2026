# Instagram SSL Pinning Bypass — Android

A pre-patched Instagram APK with SSL certificate pinning disabled for authorized security testing, debugging, and application research.

The patched APK allows supported HTTPS traffic to be inspected using tools such as Burp Suite, mitmproxy, Reqable, and Proxypin.

> **No root, Frida, or Magisk required.**
> The SSL pinning bypass is integrated directly into the APK.

---

## Features

* SSL certificate pinning disabled
* User-installed CA certificates supported
* No root access required
* No Frida scripts required
* No Magisk modules required
* Compatible with physical Android devices
* Compatible with popular Android emulators
* Works with common MITM proxy tools
* Supports `arm64-v8a` and `x86_64` builds

---

## How It Works

Instagram uses multiple layers of HTTPS protection.

### 1. Android Network Security Configuration

The application may restrict trusted certificate authorities to system-installed CA certificates, preventing certificates installed by the user from being trusted.

### 2. Application-Level Certificate Pinning

Instagram may use components such as:

* `CertificatePinner`
* `TrustManager`
* Custom certificate verifiers
* Native certificate validation
* Hardcoded certificate or public-key checks

These checks can reject traffic intercepted by a debugging proxy, even when the proxy CA certificate is installed on the device.

### Patch Changes

The patched APK modifies the relevant certificate-validation behavior by:

* Allowing user-installed CA certificates
* Enabling pin overrides where applicable
* Neutralizing supported certificate-pinning checks
* Bypassing selected custom verification methods

When the device and proxy are configured correctly, supported HTTPS traffic can be viewed through the proxy.

---

## What You Can Inspect

Depending on the Instagram version, device, and endpoint, you may be able to inspect:

* REST API requests and responses
* GraphQL queries
* Feed requests
* Stories requests
* Search requests
* Direct-message requests
* Media and CDN URLs
* Authentication flows
* Session-related requests
* Analytics events
* Tracking events
* Error responses
* Application configuration requests

> Some traffic may still use additional native protections, encryption, compression, binary formats, or transport-level mechanisms.

---

## Installation

Before installing the patched APK, you may need to uninstall the official Instagram application.

```bash
adb uninstall com.instagram.android
```

Install the patched APK:

```bash
adb install instagram-patched.apk
```

To replace an existing compatible build:

```bash
adb install -r instagram-patched.apk
```

> Patched APKs are signed with a different certificate from the official Instagram APK. Android may therefore prevent installation over the official version.

---

## Physical Android Device Setup

1. Install the patched Instagram APK.
2. Connect the Android device and computer to the same Wi-Fi network.
3. Find the computer's local IP address.
4. Configure the Android Wi-Fi proxy:

   * Proxy host: your computer's local IP address
   * Proxy port: `8080`
5. Install the proxy tool's CA certificate on the Android device.
6. Start the proxy listener.
7. Open Instagram.
8. Confirm that requests appear in the proxy.

Example mitmweb command:

```bash
mitmweb --listen-host 0.0.0.0 --listen-port 8080
```

Example mitmproxy command:

```bash
mitmproxy --listen-host 0.0.0.0 --listen-port 8080
```

---

## Android Emulator Setup

1. Install the patched APK on the emulator.
2. Configure the emulator to use the host computer's proxy.
3. Install the proxy CA certificate inside the emulator.
4. Start the proxy tool.
5. Launch Instagram.
6. Check the proxy history for captured requests.

Compatible emulator options may include:

* Android Studio Emulator
* NoxPlayer
* LDPlayer
* BlueStacks

### ADB Proxy Configuration

Set the Android proxy:

```bash
adb shell settings put global http_proxy YOUR_PC_IP:8080
```

Example:

```bash
adb shell settings put global http_proxy 192.168.1.100:8080
```

Remove the proxy configuration:

```bash
adb shell settings put global http_proxy :0
```

---

## Compatible Proxy Tools

| Tool       | Type                                 | Website       |
| ---------- | ------------------------------------ | ------------- |
| Burp Suite | Desktop security-testing proxy       | PortSwigger   |
| mitmproxy  | Open-source CLI and Web UI           | mitmproxy.org |
| Reqable    | Desktop and mobile traffic inspector | Reqable       |
| Proxypin   | Lightweight traffic-capture tool     | GitHub        |

---

## Supported Builds

| Instagram Version | Architecture          | Status                     |
| ----------------- | --------------------- | -------------------------- |
| `435.0.0.37.76`   | `arm64-v8a`, `x86_64` | Available through Telegram |
| `370.1.0.43.96`   | `arm64-v8a`, `x86_64` | Demo available in Releases |

Newer versions may be patched upon request.

---

## Download

Demo builds may be published under the repository's **Releases** section.

For the latest build or a custom Instagram version request:

**Telegram:** `https://t.me/YOUR_USERNAME`

Replace `YOUR_USERNAME` with your actual Telegram username.

---

## Troubleshooting

### No Traffic Appears

Check that:

* The phone and computer are connected to the same network
* The proxy IP address is correct
* The proxy is listening on `0.0.0.0`
* The selected port is not blocked by the firewall
* The CA certificate is installed
* Instagram is using the patched APK
* A VPN is not bypassing the Wi-Fi proxy
* Private DNS is not interfering with traffic

On Windows, allow the proxy port through the firewall or temporarily test with the firewall disabled.

### Connection Refused

Confirm that the proxy is running:

```bash
mitmweb --listen-host 0.0.0.0 --listen-port 8080
```

Verify the computer's IP address:

```powershell
ipconfig
```

Use the IPv4 address assigned to the computer's active Wi-Fi or Ethernet adapter.

Do not normally use:

* `127.0.0.1`
* A WSL virtual adapter address
* A Hyper-V virtual adapter address
* An inactive Ethernet adapter address

### Certificate Errors

Remove old proxy certificates and install the certificate generated by the proxy tool currently being used.

For mitmproxy, open the following address from the proxied Android device:

```text
mitm.it
```

Then install the Android certificate.

### App Does Not Install

The official application and patched APK may have different signing certificates.

Uninstall the existing application first:

```bash
adb uninstall com.instagram.android
```

Then install the patched build:

```bash
adb install instagram-patched.apk
```

---

## Related Projects

* TikTok SSL Pinning Bypass
* Snapchat SSL Pinning Bypass
* Threads SSL Pinning Bypass
* Facebook SSL Pinning Bypass
* Messenger SSL Pinning Bypass

---

## Legal Disclaimer

This repository is intended only for:

* Authorized security testing
* Application debugging
* Educational research
* Interoperability testing
* Testing applications and devices that you own
* Testing systems for which you have explicit permission

Do not use this project to access private communications, authentication credentials, accounts, devices, or network traffic without authorization.

You are responsible for complying with all applicable laws, platform terms, privacy requirements, and security-testing agreements.

The repository owner is not responsible for misuse of the software or information provided.

---

## Contact

For build requests, supported-version questions, or technical assistance:

**Telegram:** `https://t.me/YOUR_USERNAME`
