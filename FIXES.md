# 🛠️ EerkAI: Constraints, Errors & Fixes

This document outlines the specific hardware/software constraints imposed by Google Chrome and the engineered solutions EerkAI uses to bypass them.

---

## 1. System Constraints

| Parameter | Official Requirement | EerkAI Verified Constraint | Status |
| :--- | :--- | :--- | :--- |
| **GPU VRAM** | Minimum **3 GB** | **1.9 GB** (Integrated Graphics) | ✅ **BYPASSED** |
| **Storage** | 22 GB Free Space | >10 GB Free Space | ⚠️ **REQUIRED** |
| **Region** | US Only | Global (India/Europe) | ✅ **BYPASSED** |
| **Network** | Unmetered Wi-Fi | Any Connection | ✅ **BYPASSED** |

---

## 2. Common Errors & Solutions

### 🔴 Error 1: "Install Not Complete" / Download Stuck at 0%
**The Cause:** Geo-blocking. Google's download servers reject requests from non-US IP addresses.
**The Fix:**
1.  Go to `chrome://settings/languages`.
2.  Add **English (United States)** and move it to the top.
3.  Click the 3 dots -> **"Display Google Chrome in this language"**.
4.  **Connect to a VPN (US Server)**.
5.  Go to `chrome://components` and click "Check for Update" on *Optimization Guide On Device Model*.

### 🔴 Error 2: Model Not Found / Component Missing
**The Cause:** Hardware Gating. Chrome detected your low VRAM on startup and hid the AI features.
**The Fix:** You must perform a **Command Line Injection**.
1.  Close Chrome completely.
2.  Right-click your Chrome Dev shortcut -> **Properties**.
3.  Paste this into the **Target** field (after `chrome.exe"`):
    ```text
    --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
    ```
4.  Apply and Relaunch.

### 🔴 Error 3: Console says `window.ai is not defined`
**The Cause:** API Deprecation. In Chrome v133+, the `window.ai` namespace was removed.
**The Fix:** EerkAI v3.0 automatically handles this by targeting the new `LanguageModel` class. No user action required (ensure you are using the latest `index.html`).

### 🔴 Error 4: Red Status Dot / Input Bar Red
**The Cause:** The AI session crashed or failed to initialize (common on low RAM).
**The Fix:**
1.  Wait 3 seconds. EerkAI has an **Auto-Healing** protocol that will try to reboot the core.
2.  If it persists, check `chrome://components` to ensure the model version is not `0.0.0.0`.

---

## 3. Technical Architecture

**The Bypass Logic:**
The flag `OptimizationGuideOnDeviceModelOverride` forces the browser's "Model Installer Service" to execute regardless of the GPU check. The wildcard `*` in `performance_classes/*` tells the browser to accept "Any" hardware tier.

**The Interface Logic:**
EerkAI uses an `Async Iterator` to process text deltas (chunks) in real-time, preventing the UI from freezing while the low-spec CPU computes the answer.
