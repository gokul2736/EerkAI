# ✅ Verification Protocol 
## If EerkAI isn't working, use this checklist to diagnose the exact failure point.
### Perform these checks inside the Developer Console (F12 > Console tab).


## 🔹 Phase 1: The Flag Check (Did the hack work?)
Before doing anything, we must ensure Chrome accepted the hardware bypass.

- Open a new tab and go to: chrome://version

- Look at the Command Line section.

VERIFY: You must see this specific text inside the block: --enable-features=...OptimizationGuideOnDeviceModelOverride

❌ If missing: You didn't launch Chrome correctly. Close all windows and use your modified shortcut.

## 🔹 Phase 2: The Console Diagnostics (Deep Scan)
Perform these checks inside the Developer Console (F12 > Console tab).

Test A: Is the Brain Detected?
Copy and paste this code to see if the browser recognizes the AI API.

```javaScript
if (typeof LanguageModel !== "undefined") {
    console.log("%c✅ SUCCESS: LanguageModel API found.", "color: green; font-size: 16px; font-weight: bold;");
} else if (window.ai) {
    console.log("%c⚠️ OLD API: window.ai found (Update Chrome).", "color: orange; font-size: 16px;");
} else {
    console.log("%c❌ CRITICAL: No AI API detected. Check Flags.", "color: red; font-size: 16px; font-weight: bold;");
}
```
Test B: What is the Model Status?
Run this to see if it is downloaded, downloading, or blocked.

```JavaScript

const cap = await LanguageModel.capabilities();
console.log("Model Status: " + cap.available);
// EXPECTED OUTPUTS:
// "readily"        = INSTALLED & READY (Good)
// "after-download" = NEEDS DOWNLOAD (Connect VPN)
// "no"             = BLOCKED (Hardware or Region Lock active)
Test C: The "Defibrillator" (Force Download)
If the status is "after-download" but nothing is happening, run this to kickstart it.
```
JavaScript

console.log("🚀 Kicking the Engine...");
try {
    await LanguageModel.create({ expectedLanguage: 'en' });
    console.log("✅ Request Sent. Check chrome://components now.");
} catch (e) {
    console.log("ℹ️ Download likely started in background.");
}
## 🔹 Phase 3: The Component Check
Once the console says the request is sent, verify the file is actually writing to disk.

Go to chrome://components.

Find Optimization Guide On Device Model.

VERIFY:

Good: Version 2025.x.x.x (or similar).

Busy: Status - Downloading... (Wait for it).

Bad: Version 0.0.0.0 (Download failed. Check VPN).

## 🔹 Phase 4: The "Air-Gap" Exam (Final)
The ultimate proof.

Disconnect your Wi-Fi / Ethernet.

Open index.html.

Type: "Write a binary search function in Python."

VERIFY: If code appears on the screen while you are offline, Congratulations. You have successfully liberated the AI.
