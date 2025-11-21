# LOCAL AI
## Subject: Forced Implementation of On-Device LLM (Gemini Nano) on Sub-Optimal Hardware


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




### Behaviourial Patterns

```
This is a very common observation when moving from "Cloud AI" (like ChatGPT) to "On-Device AI" (Gemini Nano).

If you feel it is "not acting like AI," it is likely due to one of these three reasons. I have a fix for each.

Diagnosis 1: It has "Amnesia" (No Memory)
The Problem: The code I gave you creates a new brain (session) every time you click the button.

You: "My name is Sam." -> AI: "Hello Sam."

You: "What is my name?" -> AI: "I don't know." (Because it forgot the previous turn).

The Fix: We need to move the session creation outside the button click function so it "remembers" the conversation.

Diagnosis 2: It is "Too Strict"
The Problem: I set the system prompt to "Output ONLY code." If you ask "How are you?", it might try to write Python code for "How are you" or just give a blank stare because it's forced to be a coding bot.

The Fix: We will relax the instructions so it can chat and code.

Diagnosis 3: The Output looks like "Notepad"
The Problem: Real AI interfaces (like ChatGPT) highlight code in colors and format text. The current tool just dumps raw text.

The Fix: I will add a simple "Markdown Beautifier" to the HTML so code looks like code.

THE FIX: The "Smart Chat" Upgrade
Here is the Version 2.0 code. Changes:

Memory Enabled: It remembers what you said earlier.

Chat History: It shows the previous messages (User vs AI) like WhatsApp/ChatGPT.

Markdown Support: It detects code blocks (```) and colors them green.
```
