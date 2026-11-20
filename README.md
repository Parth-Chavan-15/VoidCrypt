<div align="center">

  <img src="mobile/src/main/res/drawable/logo_void.png" width="120" alt="VoidCrypt Nexus Logo" />

  # 🌑 VoidCrypt
  ### **Application-Layer Network Interceptor & Stealth Tunnel**

  <p align="center">
    <b>A high-performance Android split-tunneling client engineered for zero-configuration stealth proxying.</b><br>
    Architected by <a href="https://github.com/Parth-Chavan-15"><b>Parth Chavan</b></a> as a security-hardened fork of <a href="https://github.com/shadowsocks/shadowsocks-android">shadowsocks-android</a>.
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Security-Hardened_Nexus-blueviolet?style=for-the-badge&logo=shield&logoColor=white" alt="Security: Hardened" />
    <img src="https://img.shields.io/badge/Fork_Base-shadowsocks--android_v5.3.5-brightgreen?style=for-the-badge&logo=git&logoColor=white" alt="Fork Base" />
    <img src="https://img.shields.io/badge/Platform-Android_8.0+-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Platform" />
    <img src="https://img.shields.io/badge/Crypto-ChaCha20--Poly1305_AEAD-e25a92?style=for-the-badge&logo=shield&logoColor=white" alt="Crypto" />
    <img src="https://img.shields.io/badge/License-GPL--3.0-blue?style=for-the-badge&logo=gnu&logoColor=white" alt="License" />
  </p>

  <table align="center" width="100%">
    <tr>
      <td width="50%">
        <b>🚀 Zero-Config Nexus</b><br>
        <sub>Permanently bound to a high-speed cloud node. Tap once to establish an encrypted tunnel.</sub>
      </td>
      <td width="50%">
        <b>⚡ Omni-Scavenger Routing</b><br>
        <sub>Direct in-memory split-tunneling bypassing SQLite latency and lock contention.</sub>
      </td>
    </tr>
    <tr>
      <td width="50%">
        <b>🛡️ Stealth OS Masking</b><br>
        <sub>System notifications scrubbed under <i>"Encrypted Routing Active"</i> against shoulder-surfing.</sub>
      </td>
      <td width="50%">
        <b>🔒 Dynamic Route Lock</b><br>
        <sub>App Routing controls automatically locked & dimmed to 40% alpha during active tunnels.</sub>
      </td>
    </tr>
  </table>

</div>

---

## 👁️ Overview

**VoidCrypt** is an application-layer network interceptor designed to eliminate the **global routing overhead** found in conventional VPNs.

Standard VPNs force an entire device's traffic through an encrypted tunnel, creating high latency, thermal throttling, and bandwidth waste for applications that don't require proxying. Additionally, typical clients expose server hostnames or IP addresses in lockscreen notifications and require complex manual configuration.

VoidCrypt re-architects the Android networking pipeline into an **autonomous, zero-configuration stealth tool**:
* **Selective Application Routing:** Selectively routes targeted applications (e.g., video editing engines, browsers) through an isolated cloud endpoint.
* **Zero Overhead for Local Traffic:** Leaves games, banking apps, streaming, and background services on direct local Wi-Fi/5G for native gigabit speed.
* **Instant Out-of-the-Box Security:** Connects immediately to a dedicated cloud node running Dockerized Shadowsocks with ChaCha20-Poly1305 AEAD encryption.

---

## 🛠️ What Changed in This Fork

VoidCrypt is built upon the open-source **shadowsocks-android** (v5.3.5) codebase, heavily modified by **Parth Chavan** into a specialized, single-purpose stealth client:

* **🚀 Zero-Configuration Cloud Nexus:** Stripped out manual server configuration forms, QR code scanners, and profile import/export menus. The client is permanently hardcoded to a dedicated cloud endpoint with ChaCha20-Poly1305 AEAD encryption. Just tap the central button to connect.
* **⚡ Omni-Scavenger In-Memory Split-Tunneling:** Re-engineered the underlying routing service. Instead of relying on slow database queries that can cause split-tunnel desynchronization during startup, VoidCrypt pulls routing rules directly from in-memory application preferences with multi-delimiter parsing and automatic loopback prevention.
* **🛡️ Anti-Surveillance Notification Shielding:** Standard clients display the connected server's hostname or IP directly on Android's lockscreen and status bar. VoidCrypt scrubs all endpoint metadata from system notifications, masking the service under the uniform label `"Encrypted Routing Active"`.
* **🔒 Dynamic Route Safety Lock:** Modifying split-tunnel rules while a tunnel is active can cause packet drops and socket leaks. VoidCrypt actively monitors tunnel state and automatically disables and dims the App Routing controls (to 40% opacity) while connected.
* **🎨 AMOLED Obsidian Interface:** Replaced the legacy multi-tab list layout with a custom cyber-minimalist AMOLED interface (`#000000` deep black, `#1a0b2e` obsidian, `#e25a92` neon accent), featuring an elevated one-tap Nexus button and real-time upload/download telemetry (`StatsBar`).
* **💻 Cross-Platform Build Support:** Updated the native Cargo/NDK build toolchain to automatically detect both `python` and `python3`, ensuring clean compilation across Windows, macOS, and Linux.

---

## 🧩 Architecture & Flowcharts

> [!TIP]
> **Interactive Architecture Blueprints:** Click the sections below to expand full-color diagrams illustrating kernel-level split-tunneling and the live tunnel safety lock.

<details>
<summary>🌐 <b>Flowchart: Traffic & Split-Tunneling Pipeline</b></summary>

```mermaid
flowchart TD
    subgraph INGRESS["📱 Device Traffic"]
        APP["📱 Installed Android Apps<br/><i>(All network-bound application traffic)</i>"]
    end

    subgraph ENGINE["⚡ Omni-Scavenger Router"]
        FILTER{"⚡ Split-Tunnel Filter<br/><i>(In-Memory App Rules)</i>"}
    end

    subgraph PATHS["🔀 Dual Routing Pathways"]
        DIRECT["🚀 Direct Local Gateway<br/><b>Bypassed Apps</b> <i>(Games, Banking, Media)</i><br/>• Full Wi-Fi / 5G speed<br/>• Zero latency overhead"]
        TUN["🛡️ Virtual TUN Interface<br/><b>Selected Apps</b> <i>(Targeted Tools)</i><br/>• Android tun0 adapter<br/>• L3 IP packet capture"]
    end

    subgraph CORE["⚙️ Native Cryptographic Core"]
        NATIVE["⚙️ Native C++ & Rust Daemons<br/>• <b>tun2socks:</b> L3 to SOCKS5 translation<br/>• <b>sslocal:</b> ChaCha20-Poly1305 encryption"]
    end

    subgraph CLOUD["☁️ Cloud Nexus"]
        NODE["☁️ Dedicated Cloud Nexus Node<br/><i>(AWS Cloud Instance)</i><br/>• Secure decapsulation & forward"]
        WEB["🌐 Target Web Services"]
    end

    APP --> FILTER
    FILTER -->|"Unselected (Bypassed)"| DIRECT
    FILTER -->|"Selected (Proxied)"| TUN
    TUN --> NATIVE
    NATIVE -->|"ChaCha20-Poly1305 Stream"| NODE
    NODE --> WEB

    classDef ingress fill:#121d2f,stroke:#388bfd,stroke-width:2px,color:#ffffff;
    classDef filter fill:#2d1238,stroke:#e25a92,stroke-width:2px,color:#ffffff;
    classDef direct fill:#0f2d1e,stroke:#2ea043,stroke-width:2px,color:#ffffff;
    classDef tun fill:#1c173b,stroke:#a371f7,stroke-width:2px,color:#ffffff;
    classDef core fill:#231942,stroke:#bc52ff,stroke-width:2px,color:#ffffff;
    classDef cloud fill:#2d1a00,stroke:#ff9900,stroke-width:2px,color:#ffffff;
    classDef web fill:#082435,stroke:#00d2ff,stroke-width:2px,color:#ffffff;

    class APP ingress;
    class FILTER filter;
    class DIRECT direct;
    class TUN tun;
    class NATIVE core;
    class NODE cloud;
    class WEB web;
```

</details>

<details>
<summary>🔒 <b>Flowchart: Tunnel Lifecycle & UI Safety Lock</b></summary>

```mermaid
flowchart TD
    STANDBY["🔴 Standby (Idle State)<br/>━━━━━━━━━━━━━━━━━━━━━<br/>• Obsidian AMOLED HUD Ready<br/>• App Routing Card: <b>ENABLED</b><br/>• Network Telemetry: <b>0 B/s</b>"]
    
    STANDBY -->|"👆 User Taps Central Nexus Button"| CONNECT["⚡ Initializing Tunnel<br/>━━━━━━━━━━━━━━━━━━━━━<br/>• Inject in-memory split-tunnel rules<br/>• Pass TUN file descriptor via libancillary<br/>• Launch native tun2socks & sslocal daemons"]
    
    CONNECT --> ACTIVE["🟢 Encrypted Tunnel Active<br/>━━━━━━━━━━━━━━━━━━━━━<br/>• ChaCha20-Poly1305 encryption live<br/>• System notification: 'Encrypted Routing Active'<br/>• Live Tx / Rx bandwidth streaming"]
    
    ACTIVE --> GUARD["🔒 Active Route Safety Guard<br/>━━━━━━━━━━━━━━━━━━━━━<br/>• App Routing Card <b>LOCKED & DIMMED (40% Alpha)</b><br/>• Prevents in-flight routing table corruption"]
    
    GUARD -->|"👆 User Taps Button to Disconnect"| TEARDOWN["🛑 Teardown & Cleanup<br/>━━━━━━━━━━━━━━━━━━━━━<br/>• SIGKILL native process pool<br/>• Close virtual TUN adapter<br/>• Persist traffic statistics"]
    
    TEARDOWN --> STANDBY

    classDef standby fill:#241417,stroke:#f85149,stroke-width:2px,color:#ffffff;
    classDef connect fill:#1e1a38,stroke:#a371f7,stroke-width:2px,color:#ffffff;
    classDef active fill:#0d261a,stroke:#2ea043,stroke-width:2px,color:#ffffff;
    classDef guard fill:#33112a,stroke:#e25a92,stroke-width:2.5px,color:#ffffff;
    classDef teardown fill:#261821,stroke:#d29922,stroke-width:2px,color:#ffffff;

    class STANDBY standby;
    class CONNECT connect;
    class ACTIVE active;
    class GUARD guard;
    class TEARDOWN teardown;
```

</details>

---

## ⚙️ Quick Build Guide

Because VoidCrypt compiles native C++ and Rust networking binaries, submodules must be cloned recursively.

### 1. Prerequisites
* **Android Studio** (with NDK installed via SDK Manager)
* **JDK 17+**
* **Rust** ([rustup.rs](https://rustup.rs/))
* **Python 3**

### 2. Configure Rust Targets
Install the required Android cross-compilation targets:
```bash
rustup target add armv7-linux-androideabi aarch64-linux-android i686-linux-android x86_64-linux-android
```

### 3. Clone Repository
```bash
# Clone with all native submodules
git clone --recurse-submodules https://github.com/Parth-Chavan-15/VoidCrypt.git
cd VoidCrypt
```

*(If cloned without `--recurse-submodules`, run `git submodule update --init --recursive` inside the folder).*

### 4. Build APK
```bash
# Linux / macOS
./gradlew assembleDebug

# Windows PowerShell
.\gradlew.bat assembleDebug
```

The debug APK will be generated at `mobile/build/outputs/apk/debug/mobile-debug.apk`.

---

## 🙏 Acknowledgments & Credits

VoidCrypt is built upon the open-source work of the privacy and networking community:

* **[shadowsocks/shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android):** Base Android client and UI architecture created by **Max Lv**, **Mygod Studio**, and contributors.
* **[shadowsocks/shadowsocks-rust](https://github.com/shadowsocks/shadowsocks-rust):** High-performance Rust local proxy daemon (`sslocal`).
* **[badvpn / tun2socks](https://github.com/shadowsocks/badvpn):** L3-to-SOCKS5 packet translation bridge.
* **libancillary & libevent:** UNIX domain socket FD passing and event scheduling.

---

## ⚖️ License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**, preserving the original upstream license. See [`LICENSE`](LICENSE) for details.

Developed and maintained by **Parth Chavan** ([@Parth-Chavan-15](https://github.com/Parth-Chavan-15)).
