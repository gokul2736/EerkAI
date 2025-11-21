# 🛠️ EerkAI Setup Guide (The Bypass)

Standard Chrome blocks offline AI if you have less than **3GB VRAM** or live outside the US. Follow this guide to force-enable it.

---

## 🔹 Phase 1: The Hardware Override
*Goal: Force Chrome to ignore your laptop's specs.*

1.  Download and install **Chrome Dev** or **Canary** (Version 133+).
2.  **Close Chrome completely.** (Check Taskbar to be sure).
3.  Right-click your **Chrome Dev shortcut** > **Properties**.
4.  Find the **Target** field. Add a space at the very end, then paste the content of `flags.txt`:
    ```text
    --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
    ```
5.  Click **Apply** and **OK**.

### ✅ Checkpoint 1: Did it work?
Open Chrome Dev, open a new tab, and go to `chrome://version`.
Look at the **Command Line** box.
* **Success:** You see the text `--enable-features=...` inside the box.
* **Failure:** You only see `chrome.exe`.
    * **❌ The Fix:** You likely have a "zombie" Chrome process running. Restart your computer and try adding the flags again.

---

## 🔹 Phase 2: The Download (Region Bypass)
*Goal: Trick Google servers into giving you the 1.5GB model file.*

**⚠️ Critical:** If you are outside the US (e.g., India, UK), do not skip this.

1.  **VPN:** Connect to a **US Server** (ProtonVPN Free / Windscribe work well).
2.  **Language:**
    * Go to `chrome://settings/languages`.
    * Add **English (United States)**.
    * Click the 3 dots next to it -> **"Display Google Chrome in this language"**.
    * Click **Relaunch**.
3.  **Trigger Download:**
    * Go to `chrome://components`.
    * Find **Optimization Guide On Device Model**.
    * Click **Check for Update**.

### ✅ Checkpoint 2: Is it downloading?
Look at the status under "Optimization Guide On Device Model".
* **Success:** It says `Downloading...` or shows a version number (e.g., `2025.x.x.x`).
* **Failure A:** It says `Status - Update error` or `Install Not Complete`.
    * **❌ The Fix:** Your VPN is leaking, or you didn't set English (US) as the **Display** language. Retry Step 2.
* **Failure B:** The component isn't there at all.
    * **❌ The Fix:** The hardware override failed. Go back to **Phase 1** and fix your shortcut.

> **Note:** Once the version number appears, **disconnect your VPN**. You are now offline-ready.

---

## 🔹 Phase 3: Launching EerkAI
*Goal: Connect the interface to the brain.*

1.  Download `index.html` from this repository.
2.  Drag and drop the file into your modified Chrome Dev window.
3.  Look at the top right status.

### ✅ Checkpoint 3: System Status
* **Success:** Status says **"SYSTEM READY"** (Green Glow).
* **Failure:** Status says **"CONNECTION ERROR"** (Red Glow) or Input bar is Red.
    * **❌ The Fix:** The model is not fully loaded yet.
    * **Action:** Open Console (`F12`), type `await window.ai.languageModel.create()`, and press Enter. If it errors, your browser version is too old (Update Chrome Dev).

---

## 🎯 Final Verification
1.  Turn off your Wi-Fi.
2.  Type "Hello" in EerkAI.
3.  If it replies, you have successfully hacked the system.
