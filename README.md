<div align="center">
  
  # 🌑 VoidCrypt
  **Absolute Anonymity. Zero Compromise.**

  <p align="center">
    A streamlined, hardcoded, stealth-focused VPN client engineered for zero-configuration anonymity.
  </p>

</div>

---

## 👁️ Overview
VoidCrypt is a highly specialized networking tool designed to establish an encrypted tunnel instantly upon launch. Unlike traditional VPN clients that require manual server configuration, QR code scanning, or profile management, VoidCrypt is strictly hardcoded to a single, secure nexus node. 

The application architecture has been heavily modified from its original source to remove all user-facing configuration, resulting in a frictionless, one-tap stealth protocol.

## 🛠️ Architectural Modifications & Features
* **Zero-Config Hardcoded Engine:** Bypassed the native SQLite profile creation screens. The core routing engine is permanently bound to a designated secure node.
* **Omni-Scavenger Routing Engine:** Rewrote the `VpnService` bridging logic. VoidCrypt bypasses standard database writes, pulling per-app routing rules directly from Android `DataStore` memory for flawless split-tunneling.
* **Stealth OS Integration:** Scrubbed all exposed IP addresses from Android's foreground services. System notifications are masked under the "VoidCrypt" title to prevent network surveillance and shoulder-surfing.
* **Locked-Down UI:** Stripped out import/export menus, multi-profile selection, and extraneous settings to protect the integrity of the hardcoded tunnel.

---

## ⚙️ Build & Deployment (V2 Setup)
Because VoidCrypt relies on a custom-compiled C++ and Rust cryptographic engine, a standard `git clone` will fail. You must pull the underlying submodules and configure the native environment.

### 1. Prerequisites
* **Android Studio** (with Android NDK installed via SDK Manager)
* **JDK 11+**
* **Rust** (Required to compile the native networking binaries)

### 2. Configure Rust Targets
Before building, you must install the Android targets for Rust. Open your terminal and run:
```bash
rustup target add armv7-linux-androideabi aarch64-linux-android i686-linux-android x86_64-linux-android
```

### 3. Clone the Repository
You must use the recursive flag to pull the native engine submodules.
```bash
git clone --recurse-submodules [https://github.com/Parth-Chavan-15/VoidCrypt.git](https://github.com/Parth-Chavan-15/VoidCrypt.git)
(If you already cloned it without the flag, run git submodule update --init --recursive inside the project folder).
```

### 4. Compile
Open the folder in Android Studio, allow Gradle to sync, and build the APK.


## ⚖️ Acknowledgments & License
Developed and maintained by Parth Chavan.

This project is a heavily modified, hardcoded fork of the open-source shadowsocks-android client. All core cryptographic engine components, native C++ networking binaries, and original base architecture credits belong to the shadowsocks maintainers.

Licensed under the GPL-3.0 License. See the LICENSE file for details.
