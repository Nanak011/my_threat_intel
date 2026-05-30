# V1 of **[threat_intel](https://github.com/Nanak011/threat_intel)**

# ARCHIVED: Single-Node Honeypot Project

This repository contains the initial, single-node prototype of Threat Intel honeypot. It is preserved here as a historical archive to document the initial prototype that inspired a completely overhauled, enterprise-grade architecture.

### What Went Wrong & Operational Hurdles

1. **Local File-Splitting Faults:** The original Python script used relative pathing (`with open("raw_attacks.log")`). When running under different cron contexts, it caused the data stream to fracture into separate files across directories rather than appending to a single centralized baseline.
2. **Rate-Limiting (429/503 Faults):** Relying on a direct, unmanaged public API pipeline meant aggressive socket-flooding attacks quickly exhausted minute-to-minute API quotas, dropping vital analysis loops during traffic spikes.
3. **Single-Node Blindspot:** A single cloud instance could only capture localized internet noise, missing the broader context of global coordinated botnet tracking.

---

### What I Fixed in the New Production Version

I completely deprecated this file-based architecture and built a distributed, production-grade network.

The new system fixes these prototype issues through:
* **Global Distributed Edge Nodes:** Moved from one single droplet to a multi-node edge network running in London, New York, and Bangalore.
* **Robust Database Layer:** Replaced vulnerable flat log files with a secure PostgreSQL database via Supabase to centralize telemetry streams seamlessly.
* **Enterprise Ingestion Automation:** Shifted processing logic entirely to a background GitHub Actions runner operating on a resilient state-tracking cron loop.
* **Deduplication Hashing:** Designed an analytical filter that hashes attack metrics (`IP | Class | Location`) to consolidate script-spam and optimize system loads.

### View the Live Multi-Node Project
The upgraded architecture, live visualization dashboard, and optimized code are actively maintained here:

**[New Multi-Node Threat Intel Network & Dashboard](https://nanak011.github.io/threat_intel/)**
