# 🗺️ Anvesha AI Analyzer – Roadmap

This document outlines the development roadmap for the **Anvesha AI Analyzer**—
a privacy-first, local-AI powered browser extension and the foundation of the
future Anvesha Browser.

---

# 🚀 Phase 1 — Browser Extension (Current)

## 🎯 Objective
Deliver a fully functional **offline AI analyzer** with:
- Rust → WASM sanitization firewall  
- Local WebGPU LLM (WebLLM)  
- Transformers.js fallback  
- Complete UI  
- Risk scoring  
- IndexedDB model storage  

---

# 📌 Milestone 1 — Core Infrastructure (Week 1–2)
**Status:** In progress

### Tasks
- Finalize folder & project structure  
- Implement Rust → WASM build system  
- Write sanitization rules document  
- Define risk scoring model  
- Write Rust sanitizer structure (extract, normalize, detect)  
- Create background, content script, and messaging pipeline  
- Implement AI engine detection (WebLLM → Transformers.js → none)  
- Define extension permissions & manifest structure  

---

# 📌 Milestone 2 — Sanitizer Engine (Week 2–3)

### Rust-WASM Engine
- HTML content extraction (browser-side)
- Hidden text detection (CSS selector rules)
- Remove/comment/script/SVG/base64 blocks
- Unicode normalization (NFKC + homoglyph removal)
- Prompt injection pattern detection
- Compute risk score
- Generate structured JSON output

### Output
{
“clean_text”: “…”,
“removed_items”: {…},
“risk_score”: 0-100,
“categories”: {…}
}

---

# 📌 Milestone 3 — Local AI Engine (Week 3–4)

### Tasks
- Integrate WebLLM as primary LLM engine  
- Implement Transformers.js fallback engine  
- Load quantized models into IndexedDB  
- Add chunking logic for large pages  
- Implement JSON-based prompt templates  
- Add throttling and timeout strategies  
- Add structured summary + reasoning output  

---

# 📌 Milestone 4 — UI & UX (Week 4–5)

### Features
- Popup UI  
- Summary tab  
- Risk analysis tab  
- "What Was Removed" tab  
- Model loading indicator  
- Clear & modern design  
- Per-domain risk display  
- Page overlay (optional)

---

# 📌 Milestone 5 — Testing & Optimization (Week 5–6)

### Tasks
- Compare performance: WebLLM vs Transformers.js  
- Test sanitizer on 50+ real webpages  
- Validate risk scoring correctness  
- Cache model metadata in IndexedDB  
- Improve UI responsiveness  
- Add error logs & failure recovery  
- Add mode: "Sanitizer Only" (no LLM)  

---

# 📌 Milestone 6 — Version 1.0 Release (Week 6)

### Deliverables
- Fully working local LLM browser extension  
- WASM sanitization firewall perfected  
- Model manager + storage  
- UI polished  
- Documentation + demo videos  
- Publish to GitHub  
- Optional: Publish alpha extension privately

---

# 🌐 Phase 2 — Anvesha Native Browser (Post-extension)

## 🎯 Objective  
Transform the extension into a **full native browser** with:
- Embedded Rust LLM runtime (llama.cpp/rustformers)  
- Vulkan/Metal GPU acceleration  
- Native Rust sanitization (10–100× faster)  
- Local Tantivy search engine integration  
- Native AI tools & panels  
- Complete offline-first AI browser  

---

# 📌 Phase 2 Milestones

### 🔹 Milestone A — Browser Base (CEF + Rust)
- Create a CEF-based custom browser shell  
- Integrate Rust backend with IPC  
- Replace WASM sanitizer with native Rust engine  
- Integrate llama.cpp for native GPU LLM  

### 🔹 Milestone B — Search Engine Integration
- Integrate Tantivy indexer  
- Add RAG and embeddings  
- Native document search  
- Offline semantic search  

### 🔹 Milestone C — AI Firewall 2.0
- Native multi-thread sanitizer (Rayon)  
- DNS-level threat detection  
- Inline threat warning system  

### 🔹 Milestone D — Anvesha Browser Alpha
- Tabs  
- Local browsing  
- AI overlay  
- Summary-on-hover  
- All offline  
- Privacy-first  

---

# 🔥 Phase 3 — Full Ecosystem

### Future expansions:
- Local vector DB  
- Local personalization (never leaves device)  
- Device-level AI context manager  
- Native plugins/extensions  
- Secure memory vault  
- LLM-powered local developer tools  

---

# 🏁 Vision

> **Anvesha is the world’s first true privacy-native, fully local AI browser —  
with built-in on-device LLMs, zero cloud dependencies, and a  
multi-layer AI firewall.**

---

# End of Roadmap
