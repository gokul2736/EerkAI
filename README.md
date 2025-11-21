# -Local-AI-Low-Spec

```
📔 RESEARCH LOG: PROJECT NEURAL-BYPASSSubject: Forced Implementation of On-Device LLM (Gemini Nano) on Sub-Optimal HardwareDate: November 21, 2025Researcher: [Your Name]1. THE OBJECTIVETo achieve "Air-Gapped" (Offline) AI inference capabilities within a web browser environment, enabling secure code generation and automation without sending data to cloud servers.2. SYSTEM CONSTRAINTS & REQUIREMENTSThe primary challenge was overcoming the hard-coded restrictions in the Chromium engine.ParameterOfficial RequirementMy System (The Constraint)StatusGPU VRAMMinimum 3 GB dedicated1.9 GB (Integrated/Low-End)❌ FAILEDStorage> 22 GB Free Space172 GB Free Space✅ PASSEDRegionUS / Select CountriesIndia (IN)❌ BLOCKEDBrowserChrome Canary/DevChrome Dev v133+⚠️ VOLATILENetworkUnmetered Wi-FiStandard Wi-Fi✅ PASSED3. THE TECHNICAL BARRIERSHardware Lock: Chrome automatically aborts the model download if VRAM < 3GB.Geo-Block: Download servers reject requests from non-US IP addresses.API Deprecation: The standard window.ai documentation is obsolete in v133+ builds; the namespace has shifted to LanguageModel.4. THE ENGINEERED SOLUTION (Methodology)A. The Hardware Override (Command Injection)To bypass the VRAM check, the standard browser shortcut was modified to inject specific feature flags at runtime.Code: --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverrideNote: The * wildcard forces compatibility with ALL hardware classes. The Override tag prevents the "Install Not Complete" error on low VRAM.B. The Region SpoofingBrowser Level: Display Language set strictly to English (United States).Network Level: VPN tunneling to US-West during the initial 1.5GB payload acquisition.C. API Interface (The "Bridge")The standard window.ai.createTextSession() failed due to version mismatch.Discovery: Detected hidden global class LanguageModel.Implementation: Constructed a custom asynchronous handler to stream "deltas" (chunks) of text rather than full replacements, solving the "jumping text" UI glitch.5. FINAL CONFIGURATIONModel Version: 2025.8.21.1028 (1.5 Billion Parameters).Interface: Custom HTML5 Dashboard ("Offline Architect").Latency: 0ms Network / ~30s Cold Start / Instant Token Generation.🐙 GitHub Repository PlanSince you are making this public to help friends, here is how you should structure the repo.Repo Name Ideas:Chrome-Nano-UnlockerLow-Spec-Local-AIProject-Offline-ArchitectFile Structure:Plaintext📂 Chrome-Nano-Unlocker/
├── 📄 offline-architect.html      (The UI code we wrote)
├── 📄 launch-chrome.bat           (A script to open Chrome with flags automatically)
├── 📄 README.md                   (The instructions)
└── 📂 screenshots/                (Images of it working offline)
What to put in the README.md (The Guide):I have written the "About" section for you. You can paste this right into your GitHub:## About This ProjectThis repository provides a method to run Google's Gemini Nano AI locally and offline in Chrome, specifically optimized for low-end laptops (under 3GB VRAM) and restricted regions (outside the US).## Why use this?Privacy: Your code/prompts never leave your laptop.Zero Latency: Works without internet.Free: No API keys required.## The "Magic" CommandTo bypass the GPU requirements, you must launch Chrome with these flags:chrome.exe --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
```
vdnvdsn

```
📔 Research Log: Project Zero-Latency
Date: November 21, 2025 Location: Kuthambakkam, IN Objective: Establish offline Artificial Intelligence capabilities on restricted hardware (Low VRAM).

Technical Constraints:

Hardware: 1.9 GB VRAM (Required: 3 GB).

Software: Chrome Dev v133+ (Bleeding Edge).

Blockers: Geo-IP Lock (India), Hardware Incompatibility, API Deprecation (window.ai removed).

Execution Log:

Hardware Bypass: Utilized Command Line Injection (--enable-features=...OptimizationGuideOnDeviceModelOverride) to force the browser to ignore the 3GB VRAM requirement.

Region Bypass: Overcame Geo-blocking via Language Settings (US English) and VPN tunneling during initial payload download (1.5 GB).

API Reverse Engineering: Identified the new LanguageModel class in Chrome v133, replacing the deprecated window.ai method.

Interface: Developed "Offline Architect," a single-file HTML/JS dashboard to interface with the local model for secure code generation.

Result: Successful deployment of Gemini Nano (1.5B parameters) running locally. System generates code/configs with 0ms network latency and complete privacy.

Status: OPERATIONAL

🐙 GitHub Repo Advice
For your repository, I suggest a name like "Chrome-Nano-Unleashed" or "Local-AI-Low-Spec".

What to include in your README.md:

The Shortcut Target: (The magic code we used).

The Flags: List the 3 flags we enabled.

The HTML File: Upload your offline-architect.html so people have a UI to use immediately.

The "India Fix": Mention the Language setting + VPN tip, as that is crucial for students here.
```




# Chrome Nano Unlocker (Local AI Sidepanel)

A research project to force-enable Google's Gemini Nano AI on low-end hardware (under 3GB VRAM) and restricted regions. This extension runs **completely offline**.

## 🚀 Features
- **Zero Latency:** Generates code/text instantly on your device.
- **Privacy First:** No data leaves your laptop.
- **Hardware Bypass:** runs on integrated graphics (tested on 1.9GB VRAM).

## 🛠️ Installation Guide

### 1. The Browser Setup (Crucial)
You must launch Chrome Dev with specific flags to unlock the AI model.
1. Right-click your Chrome Dev shortcut -> **Properties**.
2. Add this to the **Target** field:
   `--enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride`

### 2. The "India Fix" (Region Lock)
If you are outside the US:
1. Set Chrome Language to **English (United States)**.
2. Connect to a US VPN for the initial download.

### 3. Loading the Extension
1. Clone this repo.
2. Go to `chrome://extensions`.
3. Enable **Developer Mode**.
4. Click **Load Unpacked** and select this folder.

## 📝 Usage
Click the extension icon to open the AI Sidepanel. Use the **NUKE_DATA** button to instantly wipe the session and clear memory.




