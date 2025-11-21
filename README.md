# Eerk-AI
 **E**ncrypted **E**ngine **R**esearch **K**it -**AI**

## Subject: Forced Implementation of On-Device LLM (Gemini Nano) on Sub-Optimal Hardware

**EerkAI** is a specialized interface that forces Google's **Gemini Nano LLM** to run locally on low-spec hardware (verified on **1.9GB VRAM**) and in restricted regions. It provides a distraction-free, modern chat interface that runs **100% offline**.

![Status](https://img.shields.io/badge/Status-Operational-brightgreen) ![Privacy](https://img.shields.io/badge/Privacy-Air--Gapped-blue) ![Size](https://img.shields.io/badge/Size-4KB-orange)

### 1. THE OBJECTIVE
To achieve "Air-Gapped" (Offline) AI inference capabilities within a standard web browser environment, enabling secure code generation and automation on a student laptop without sending data to cloud servers.

### 2. SYSTEM CONSTRAINTS & REQUIREMENTS
The primary challenge was overcoming the hard-coded restrictions in the Chromium engine that block AI on non-flagship hardware.
|ParameterOfficial |Requirement|My System (The Constraint)|Status|
|------------------|-----------|--------------------------|------|
|GPU VRAM|Minimum 3 GB dedicated|1.9 GB (Integrated/Low-End)|❌ FAILED|
|Storage|> 22 GB Free Space|172 GB Free Space|✅ PASSED|
|RegionUS| / Select Countries|India (IN)|❌ BLOCKED|
|Browser|ChromeDev  |Chrome Dev v133+|⚠️ VOLATILE|
|VOLATILENetwork|Unmetered Wi-Fi|Standard Wi-Fi|✅ PASSED

### 3. THE TECHNICAL BARRIERS
- **Hardware Lock:** Chrome automatically aborts the model download if VRAM < 3GB. So of course Saveetha  laps have virtual ram of 1.9 we must Override this specific part*
- **Geo-Block:** Download servers reject requests from non-US IP addresses (IP-based filtering). 
- **API Deprecation:** The standard window.ai documentation is obsolete in v133+ builds; the namespace has shifted to LanguageModel.

### 4. THE ENGINEERED SOLUTION (Methodology)
A. The Hardware Override (Command Injection) To bypass the VRAM check, the standard browser shortcut was modified to inject specific feature flags at runtime.

- Code:
 ```
--enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
```

Note: The * wildcard forces compatibility with ALL hardware classes. The Override tag prevents the "Install Not Complete" error on low VRAM.

- B. The Region Spoofing

Browser Level: Display Language set strictly to English (United States).

Network Level: VPN tunneling to US-West during the initial 1.5GB payload acquisition.

- C. API Interface (The "Bridge")

Discovery: Detected hidden global class LanguageModel.

Implementation: Constructed a custom standalone HTML5 dashboard ("Offline Architect") to interface directly with the VRAM model. Implemented "Stealth Mode" logic to wipe execution memory instantly.

5. FINAL CONFIGURATION
Model Version: 2025.8.21.1028 (1.5 Billion Parameters).

Interface: Standalone Single-File Web App (.html).

Latency: 0ms Network / Instant Token Generation.

Status: OPERATIONAL



# EerkAI (v3.0)
### Encrypted Engine Research Kit


**EerkAI** is a specialized interface that forces Google's **Gemini Nano LLM** to run locally on low-spec hardware (verified on **1.9GB VRAM**) and in restricted regions. It provides a distraction-free, modern chat interface that runs **100% offline**.

![Status](https://img.shields.io/badge/Status-Operational-brightgreen) ![Privacy](https://img.shields.io/badge/Privacy-Air--Gapped-blue) ![VRAM](https://img.shields.io/badge/VRAM-1.9GB_Verified-orange)


## ⚡ Core Capabilities

* **🧠 Persistent Context:** The AI remembers previous turns in the conversation (no more "amnesia").
* **100% Offline:** Runs entirely in the browser via the `LanguageModel` API.
* **Auto-Healing Core:** Automatically detects frozen sessions and reboots the AI brain in milliseconds.
* **Stealth Mode (NUKE):** A dedicated Trash button instantly wipes the session, clears the screen, and flushes console logs.
* **Smart Streaming:** Smooth text generation that handles data chunks intelligently.

## 🚀 Quick Start

1.  **Download** the `index.html` file from this repository.
2.  **Configure your browser** (See [SETUP_GUIDE.md](SETUP_GUIDE.md) for the bypass instructions).
3.  **Drag and drop** `index.html` into Chrome.
4.  **Start typing.**

## 📂 Documentation
This tool requires specific browser flags to bypass hardware checks.
👉 **[READ THE SETUP GUIDE HERE](SETUP_GUIDE.md)**

## 📜 License
Open Source. Dedicated to the pursuit of knowledge.

## ⚡ Core Capabilities

* **100% Offline:** Runs entirely in the browser with zero server calls.
* **Auto-Healing Engine:** Automatically detects frozen sessions and reboots the AI core in milliseconds without refreshing the page.
* **Stealth Mode (NUKE):** One-click memory wipe that clears the screen, resets the model, and flushes console logs instantly.
* **Smart Streaming:** Handles data chunks intelligently to prevent text flickering/jumping.
* **Markdown Rendering:** Automatically formats code blocks with syntax highlighting.

## 📦 Installation

EerkAI is a **Zero-Dependency** tool. You do not need Node.js, Python, or a local server.

1.  **Download** the `index.html` file from this repository.
2.  **Drag and drop** it into your Chrome Dev browser.
3.  **Start typing.**

## 🛠️ Prerequisites

**Important:** EerkAI requires a Chromium browser with the **Gemini Nano** model enabled.
* **Browser:** Chrome Dev / Canary (v133+)
* **Flags Required:**
    * `PromptAPIForGeminiNano`
    * `OptimizationGuideOnDeviceModel`

*(If your browser is not set up yet, see `SETUP_GUIDE.md` in this repo).*

## 🖥️ Interface Controls

| Command | Action |
| :--- | :--- |
| **RUN** | Executes the prompt and streams the response. |
| **WIPE** | Instantly clears chat history and destroys the current session (Stealth Mode). |
| **Enter** | Submit command. |
| **Shift+Enter** | New line. |

## 📜 License

Open Source. Dedicated to the pursuit of knowledge.






# Software Requirements Specification: EerkAI (v3.0)

**Project Name:** Encrypted Engine Research Kit - AI (EerkAI)  
**Version:** 3.0 (Stable)  
**Status:** Operational  
**License:** Open Source (MIT)

---

## 1. Introduction

### 1.1 Purpose
The purpose of **EerkAI** is to provide a lightweight, zero-dependency interface for interacting with on-device Large Language Models (LLMs), specifically Google's Gemini Nano. It is engineered to overcome artificial hardware constraints (VRAM gating) and regional restrictions, enabling offline AI inference on standard consumer hardware.

### 1.2 Scope
The software functions as a client-side web application running within the Chromium environment. It bridges the gap between the user and the browser's internal `LanguageModel` API.
**Key Capabilities:**
* Offline text generation (Air-gapped).
* Bypassing GPU VRAM requirements (<3GB).
* Persistent session management (Context Awareness).
* Real-time Markdown rendering.

### 1.3 Definitions & Acronyms
* **LLM:** Large Language Model.
* **VRAM:** Video Random Access Memory.
* **Air-Gapped:** Isolated from unsecured networks (Internet).
* **API:** Application Programming Interface.

---

## 2. Overall Description

### 2.1 Product Perspective
EerkAI operates as a standalone HTML5 application. It does not require a backend server (Node.js, Python) or cloud dependencies. It utilizes the experimental AI capabilities embedded in Chrome Dev/Canary builds (v133+).

### 2.2 User Characteristics
* **Target Audience:** Researchers, Students, and Developers.
* **Technical Proficiency:** Intermediate (Requires ability to modify browser launch flags).

### 2.3 Hardware Constraints
* **Minimum Requirement:** Integrated GPU with shared memory.
* **Verified Testbed:** Intel UHD Graphics / 1.9 GB VRAM.
* **Storage:** 2GB free space (for model weights).

---

## 3. Specific Requirements (Functional)

### 3.1 Core Inference Engine
* **FR-01:** The system shall initialize a connection to the `window.ai.languageModel` or `LanguageModel` class upon launch.
* **FR-02:** The system shall auto-detect API availability and visually indicate status (Green/Red).
* **FR-03:** The system shall support "Auto-Healing"; if a session hangs, it must terminate and re-initialize the instance automatically.

### 3.2 User Interface
* **FR-04:** The interface shall feature a floating input dock containing the text area and action buttons.
* **FR-05:** The "Send" button must dynamically transform into a "Stop" button during active generation.
* **FR-06:** The "Theme Toggle" shall switch between Dark Mode and Light Mode and persist the user's choice via LocalStorage.

### 3.3 Data Privacy & Security
* **FR-07 (Stealth Mode):** The "NUKE" function must perform a hard reset: clearing the DOM, destroying the session object, and flushing console logs.
* **FR-08:** No data shall be transmitted over the network. All processing must remain local.

---

## 4. Installation & Configuration Guide

### 4.1 Pre-requisites
The software requires a specific environment configuration to function.

**Browser:** Google Chrome Dev or Canary (v133+)

### 4.2 Configuration (The Bypass)
To enable the underlying model on restricted hardware, the browser must be launched with specific command-line arguments.

**Steps:**
1.  Right-click the Chrome Dev shortcut.
2.  Select **Properties**.
3.  Append the following flags to the **Target** field:
    ```text
    --enable-features=PromptAPIForGeminiNano,OptimizationGuideOnDeviceModel:compatible_on_device_performance_classes/*,OptimizationGuideOnDeviceModelOverride
    ```

### 4.3 Deployment
1.  Download `index.html` from the repository release.
2.  Launch the modified Chrome Dev browser.
3.  Drag and drop the file into the browser window.

---

## 5. Interface Design

### 5.1 Chat Interface
The main view consists of a vertically scrolling chat history.
* **User Prompts:** Aligned right, styled with accent colors.
* **AI Responses:** Aligned left, rendering Markdown (Code blocks, Bold, Italics).

### 5.2 Code Block Rendering
Output detected as code (wrapped in triple backticks) is rendered in a dedicated container:
* **Header:** Displays language type (e.g., Python, JS).
* **Body:** Monospace font with syntax coloring.
* **Action:** "Copy to Clipboard" button with visual feedback.

---

## 6. Appendix

### 6.1 Technology Stack
* **Frontend:** HTML5, CSS3 (CSS Variables), Vanilla JavaScript (ES6+).
* **Backend:** N/A (Client-Side only).
* **Model:** Gemini Nano (Quantized 1.5B).

### 6.2 Known Issues
* **Cold Start:** Initial prompt may take 5-10 seconds to load into VRAM on low-end devices.
* **Context Window:** Limited by the browser's allocation (approx. 4k tokens).

---

**Developed by [Your Name]** *Dedicated to the pursuit of knowledge.*
```
