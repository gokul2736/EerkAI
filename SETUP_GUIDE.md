
## 🔹 Phase 1: The Hardware Override
*Goal: Force Chrome to ignore your laptop's specs.*

1.  Download and install **Chrome Dev** or **Canary** (Version 133+).
2.  **Close Chrome completely.** (Check Taskbar to be sure).
3.  Locate your **Chrome Dev** shortcut on the Desktop.
4.  Right-click your **Chrome Dev shortcut** > **Properties**.
5.  Look at the **Target** field. It ends with `...chrome.exe"`.
6.  **Add a space** at the very end, and paste this exact code:
    ```text
    --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
    ```
9.   ## Refer [Flags.txt](https://github.com/gokul2736/EerkAI/blob/main/flags.txt)

<img width="545" height="697" alt="Screenshot 2025-11-22 020742" src="https://github.com/user-attachments/assets/b6e91ecc-6146-4e87-8cb5-f0affedc9b05" />

7.  Click **Apply** and **OK**.
8.  Launch Chrome using this modified shortcut.

### ✅ Checkpoint 1: Did it work?
1. Open Chrome Dev, open a new tab, and go to `chrome://version`.
2. Look at the **Command Line** box.
* **Success:** You see the text `--enable-features=...` inside the box.
 <img width="757" height="162" alt="image" src="https://github.com/user-attachments/assets/4515db43-bab5-4aa3-b793-641127ff96ce" />

* **Failure:** You only see `chrome.exe`.
    * **❌ The Fix:** You likely have a "zombie" Chrome process running. Restart your computer and try adding the flags again.

---

## 🔹 Phase 2: The Download (Region Bypass) 
*Goal: Trick Google servers into giving you the 1.5GB model file.* **Google chevilo puvvu pettabothunavv simplyy**
**⚠️ Critical:** If you are outside the US (e.g., India, UK), do not skip this.

1.  **Language:**
    * Go to `chrome://settings/languages`.
    * Add **English (United States)**.
    * Click the 3 dots next to it -> **"Display Google Chrome in this language"**.
<img width="981" height="432" alt="image" src="https://github.com/user-attachments/assets/fc9f5a1d-5e53-42f9-910f-8c0f17149852" />
    * Click **Relaunch**.
      
2.  **Trigger Download:**
    * Go to `chrome://components`.
    * Find **Optimization Guide On Device Model**.
<img width="466" height="86" alt="Screenshot 2025-11-21 110544" src="https://github.com/user-attachments/assets/598cde88-f88d-47f2-bb47-af5d5aded4a6" />  
    * Click **Check for Update**.   
    * *Wait for it to finish downloading (approx 1.5GB).*


## Wait for some 5-8 min in mean tym the LLM will be downloaded to Local directory (approx 1.5GB).*


 after waiting u"ll get this  
 <img width="587" height="75" alt="Screenshot 2025-11-22 030134" src="https://github.com/user-attachments/assets/1b957221-6483-43d2-8cbd-4a0cd585e9d6" />   
 If you get this kind of output then you've finished  sucessfully  

### ✅ Checkpoint 2: Is it downloading?
Look at the status under "Optimization Guide On Device Model".
* **Success:** It says `Downloading...` or shows a version number (e.g., `2025.x.x.x`).
* **Failure A:** It says `Status - Update error` or `Install Not Complete`.
    * **❌ The Fix:** Your VPN is leaking, or you didn't set English (US) as the **Display** language. Retry Step 2.
* **Failure B:** The component isn't there at all.
    * **❌ The Fix:** The hardware override failed. Go back to **Phase 1** and fix your shortcut.

---

## 🔹 Phase 3: Launching EerkAI
*Goal: Connect the interface to the brain.*

1.  Download `index.html` from this repository.
2. Save the index.html on desktop and open it with Chrome Dev Broswer
4.  Look at the top right status.

### ✅ Checkpoint 3: System Status
* **Success:** Status says **"SYSTEM READY"** (Green Glow).
* **Failure:** Status says **"CONNECTION ERROR"** (Red Glow) or Input bar is Red.
    * **❌ The Fix:** The model is not fully loaded yet.
    * **Action:** Open Console (`F12`), type `await window.ai.languageModel.create()`, and press Enter. If it errors, your browser version is too old (Update Chrome Dev).


## 🎯 Final Verification
1.  Turn off your Wi-Fi.
2.  Type "Hello" in EerkAI.
3.  If it replies, you have successfully hacked the system.
