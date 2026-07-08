# 📱 Instagram SSL Pinning Bypass — Android

A pre-patched Instagram APK with SSL certificate pinning disabled for authorized security testing, debugging, and application research.

Inspect supported HTTPS traffic using tools such as Burp Suite, mitmproxy, Reqable, and Proxypin.

> ✅ **No root required**
> ✅ **No Frida required**
> ✅ **No Magisk required**
> ✅ **SSL bypass integrated directly into the APK**

---

## ✨ Features

* ✅ SSL certificate pinning disabled
* ✅ User-installed CA certificates supported
* ✅ No root access required
* ✅ No Frida scripts required
* ✅ No Magisk modules required
* ✅ Works on physical Android devices
* ✅ Works on popular Android emulators
* ✅ Compatible with common MITM proxy tools
* ✅ Supports `arm64-v8a` and `x86_64`
* ✅ Easy proxy configuration

---

## 🔍 How It Works

Instagram uses multiple layers of HTTPS protection.

### 1️⃣ Android Network Security Configuration

The application may restrict trusted certificate authorities to system-installed CA certificates.

This prevents user-installed proxy certificates from being trusted.

### 2️⃣ Application-Level Certificate Pinning

Instagram may use components such as:

* `CertificatePinner`
* `TrustManager`
* Custom certificate verifiers
* Native certificate validation
* Hardcoded certificate checks
* Public-key pinning

These protections may reject intercepted traffic even when the proxy CA certificate is installed.

### 🛠️ Patch Changes

The patched APK modifies the relevant certificate-validation behavior by:

* ✅ Allowing user-installed CA certificates
* ✅ Enabling pin overrides where applicable
* ✅ Neutralizing supported certificate-pinning checks
* ✅ Bypassing selected custom certificate verifiers
* ✅ Allowing HTTPS traffic through configured debugging proxies

When the device and proxy are configured correctly, supported HTTPS requests can be viewed through your proxy tool.

---

## 📡 What You Can Inspect

Depending on the Instagram version, device, endpoint, and configuration, you may be able to inspect:

* 🌐 REST API requests and responses
* 🧩 GraphQL queries
* 📰 Feed requests
* 🎞️ Stories requests
* 🔎 Search requests
* 💬 Direct-message requests
* 🖼️ Media and CDN URLs
* 🔐 Authentication flows
* 🍪 Session-related requests
* 📊 Analytics events
* 🧭 Tracking events
* ⚠️ Application error responses
* ⚙️ Configuration requests
* 🎯 Content recommendation requests

> ⚠️ Some traffic may still use additional native protections, encryption, compression, binary formats, or custom transport mechanisms.

---

## 📦 Installation

Before installing the patched APK, you may need to uninstall the official Instagram application.

```bash
adb uninstall com.instagram.android
```

Install the patched APK:

```bash
adb install instagram-patched.apk
```

Replace an existing compatible build:

```bash
adb install -r instagram-patched.apk
```

> ⚠️ Patched APKs are usually signed with a different certificate from the official Instagram APK. Android may prevent installation over the official application.

---

## 📲 Physical Android Device Setup

1. ✅ Install the patched Instagram APK.
2. ✅ Connect the Android device and computer to the same Wi-Fi network.
3. ✅ Find your computer's local IPv4 address.
4. ✅ Open the Wi-Fi proxy settings on the Android device.
5. ✅ Enter your computer's IP address as the proxy host.
6. ✅ Set the proxy port to `8080`.
7. ✅ Install the proxy tool's CA certificate.
8. ✅ Start the proxy listener.
9. ✅ Open Instagram.
10. ✅ Confirm that requests appear in the proxy.

### Example mitmweb Command

```bash
mitmweb --listen-host 0.0.0.0 --listen-port 8080
```

### Example mitmproxy Command

```bash
mitmproxy --listen-host 0.0.0.0 --listen-port 8080
```

---

## 🖥️ Android Emulator Setup

1. ✅ Install the patched APK on the emulator.
2. ✅ Configure the emulator to use the host computer's proxy.
3. ✅ Install the proxy CA certificate inside the emulator.
4. ✅ Start the proxy tool.
5. ✅ Launch Instagram.
6. ✅ Check the proxy history for captured requests.

### Supported Emulator Options

* Android Studio Emulator
* NoxPlayer
* LDPlayer
* BlueStacks

---

## ⚙️ ADB Proxy Configuration

Set the Android proxy:

```bash
adb shell settings put global http_proxy YOUR_PC_IP:8080
```

Example:

```bash
adb shell settings put global http_proxy 192.168.1.100:8080
```

Remove the proxy:

```bash
adb shell settings put global http_proxy :0
```

Check the current proxy:

```bash
adb shell settings get global http_proxy
```

---

## 🧰 Compatible Proxy Tools

| Tool       | Type                             | Status      |
| ---------- | -------------------------------- | ----------- |
| Burp Suite | Desktop security-testing proxy   | ✅ Supported |
| mitmproxy  | Open-source CLI and Web UI       | ✅ Supported |
| Reqable    | Modern traffic inspection tool   | ✅ Supported |
| Proxypin   | Lightweight traffic-capture tool | ✅ Supported |

---

## 📋 Supported Builds

| Instagram Version | Architecture          | Status                        |
| ----------------- | --------------------- | ----------------------------- |
| `435.0.0.37.76`   | `arm64-v8a`, `x86_64` | ✅ Available through Telegram  |
| `370.1.0.43.96`   | `arm64-v8a`, `x86_64` | 🧪 Demo available in Releases |

> 🔄 Newer Instagram versions may be patched upon request.

---

## ⬇️ Download

Demo builds may be published in the repository's **Releases** section.

For the latest build or a custom Instagram version request:

### 📩 Telegram

`https://t.me/YOUR_USERNAME`

> Replace `YOUR_USERNAME` with your real Telegram username.

---

## 🧪 Quick Test Checklist

Before launching Instagram, confirm the following:

* [ ] The patched APK is installed
* [ ] The phone and computer are on the same network
* [ ] The correct IPv4 address is being used
* [ ] The proxy is listening on port `8080`
* [ ] The firewall allows incoming connections
* [ ] The proxy CA certificate is installed
* [ ] The Android proxy is configured correctly
* [ ] No VPN is bypassing the Wi-Fi proxy
* [ ] Instagram is not the official unpatched build

---

## 🛠️ Troubleshooting

### ❌ No Traffic Appears

Check that:

* ✅ The phone and computer are connected to the same network
* ✅ The proxy IP address is correct
* ✅ The proxy is listening on `0.0.0.0`
* ✅ Port `8080` is not blocked
* ✅ The CA certificate is installed
* ✅ Instagram is using the patched APK
* ✅ A VPN is not bypassing the proxy
* ✅ Private DNS is not interfering with the connection

On Windows, check your network information using:

```powershell
ipconfig
```

Use the IPv4 address of your active Wi-Fi or Ethernet adapter.

Avoid using:

* ❌ `127.0.0.1`
* ❌ WSL virtual adapter addresses
* ❌ Hyper-V virtual adapter addresses
* ❌ Inactive Ethernet adapter addresses

---

### 🚫 Connection Refused

Confirm that the proxy is running:

```bash
mitmweb --listen-host 0.0.0.0 --listen-port 8080
```

Confirm that the selected port is not already in use:

```powershell
netstat -ano | findstr :8080
```

You may also need to allow port `8080` through Windows Firewall.

---

### 🔒 Certificate Errors

Remove old proxy certificates and install the certificate generated by the proxy tool currently being used.

For mitmproxy, open the following address from the proxied Android device:

```text
http://mitm.it
```

Then download and install the Android certificate.

---

### 📵 APK Does Not Install

The official Instagram application and the patched APK may have different signing certificates.

Uninstall the existing application:

```bash
adb uninstall com.instagram.android
```

Install the patched APK:

```bash
adb install instagram-patched.apk
```

---

### ⚠️ App Opens but Requests Fail

Possible causes include:

* Additional native certificate validation
* Unsupported Instagram version
* Incorrect proxy certificate
* QUIC or HTTP/3 traffic
* Binary or encrypted request payloads
* Device integrity checks
* Emulator detection
* App signature verification
* Server-side security restrictions

---

## 🚀 Related Projects

* 🎵 TikTok SSL Pinning Bypass
* 👻 Snapchat SSL Pinning Bypass
* 🧵 Threads SSL Pinning Bypass
* 📘 Facebook SSL Pinning Bypass
* 💬 Messenger SSL Pinning Bypass

---

## 📜 Legal Disclaimer

This repository is intended only for:

* ✅ Authorized security testing
* ✅ Application debugging
* ✅ Educational research
* ✅ Interoperability testing
* ✅ Testing devices and applications that you own
* ✅ Testing systems for which you have explicit permission

Do not use this project to access:

* ❌ Private communications
* ❌ Authentication credentials
* ❌ Accounts you do not own
* ❌ Devices you do not control
* ❌ Network traffic without authorization

You are responsible for complying with all applicable laws, privacy requirements, security-testing agreements, and platform terms.

The repository owner is not responsible for misuse of the software, APK files, documentation, or information provided.

---

## 📬 Contact

For build requests, supported-version questions, custom patches, or technical assistance:

### Telegram

`https://t.me/YOUR_USERNAME`

---

## ⭐ Support the Project

If this project helped you:

* ⭐ Star the repository
* 🍴 Fork the project
* 🐛 Report issues
* 💡 Suggest improvements
* 📢 Share it with other authorized security researchers
