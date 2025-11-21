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
- **Hardware Lock:** Chrome automatically aborts the model download if VRAM < 3GB.
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
