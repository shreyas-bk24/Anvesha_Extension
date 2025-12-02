Anvesha AI Analyzer — Browser Extension (Phase 1)


     ███╗   ██╗ █████╗ ██╗   ██╗███████╗███████╗██╗  ██╗
     ████╗  ██║██╔══██╗██║   ██║██╔════╝██╔════╝██║ ██╔╝
     ██╔██╗ ██║███████║██║   ██║███████╗█████╗  █████╔╝ 
     ██║╚██╗██║██╔══██║╚██╗ ██╔╝╚════██║██╔══╝  ██╔═██╗ 
     ██║ ╚████║██║  ██║ ╚████╔╝ ███████║███████╗██║  ██╗
     ╚═╝  ╚═══╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝╚══════╝╚═╝  ╚═╝

                     A N V E S H A
Local AI · Privacy‑First · Rust → WASM Sanitizer · WebGPU LLM

Overview
--------

Anvesha is a privacy-preserving, local-first AI analyzer implemented as a browser extension.
It uses a Rust → WebAssembly sanitization engine and local WebGPU-accelerated LLM inference
to analyze web content without sending data to the cloud.

Key goals for Phase 1:

- Build a secure on-device AI firewall
- Provide a local offline LLM analyzer
- Implement a sanitizer to neutralize prompt-injection attempts
- Establish a foundation for the future Anvesha Browser

Project overview
----------------

The extension:

- Extracts webpage content
- Sanitizes HTML, comments, hidden text, SVGs, scripts and base64 blobs
- Detects and neutralizes prompt-injection attacks
- Computes local risk scores
- Sends only sanitized text to a local LLM (WebLLM / WebGPU)
- Performs all analysis offline with zero cloud communication

Folder structure
----------------

```
project-root/
├── extension/                     # Browser extension root
│   ├── manifest.json
│   ├── package.json
│   ├── vite.config.js
│   └── src/
│       ├── background/
│       │   ├── background.js
│       │   ├── engine-detect.js
│       │   ├── wasm-loader.js
       │   ├── llm-engine.js
│       │   ├── model-manager.js
│       │   └── message-router.js
│       ├── content/
│       │   └── contentScript.js
│       ├── ui/
│       │   ├── popup.html
│       │   ├── popup.js
│       │   └── popup.css
│       ├── storage/
│       │   ├── idb.js
│       │   ├── settings.js
│       │   └── cache.js
│       ├── engines/
│       │   ├── webllm-engine.js
│       │   └── transformers-engine.js
│       ├── utils/
│       │   ├── logger.js
│       │   ├── message.js
│       │   └── constants.js
│       └── wasm/
│           └── sanitizer_bg.wasm   # Built WASM binary (copied from `rust-wasm/pkg`)

├── rust-wasm/                     # Rust → WASM sanitization engine
│   ├── Cargo.toml
│   ├── src/
│   │   ├── lib.rs
│   │   ├── sanitize.rs
│   │   ├── extract.rs
│   │   ├── normalize.rs
│   │   ├── patterns.rs
│   │   ├── risk.rs
│   │   ├── models.rs
│   │   └── utils.rs
│   └── pkg/                       # `wasm-pack` output
│       ├── sanitizer.js
│       ├── sanitizer_bg.wasm
│       └── sanitizer_bg.wasm.map

├── docs/                          # Technical documents
└── scripts/                       # Helper build scripts
```

Tech stack
----------

- Rust (sanitization, normalization, risk scoring)
- WebAssembly (`wasm-bindgen`) for browser execution
- WebLLM + WebGPU for local LLM inference (primary)
- Transformers.js (WASM/WebGPU) as a fallback
- IndexedDB for storing model weights and history
- Manifest V3 browser extension using Vite for bundling

Security & sanitization features
-------------------------------

- HTML/DOM extraction and sanitization
- SVG and script stripping
- Base64 decoding and sanitization
- Unicode homoglyph normalization
- Zero-width character removal
- Hidden text detection
- Regex-based prompt-injection detection
- Local risk scoring engine

Project goals (Phase 1)
-----------------------

- Build a full on-device AI analyzer
- Implement a Rust-WASM prompt-injection firewall
- Enable WebGPU-based local LLM inference
- Eliminate cloud dependencies for analysis
- Maximize on-device privacy

Future roadmap (Phase 2+)
-------------------------

Phase 2 — Anvesha Native Browser

- Chromium/CEF-based or Rust/WebView browser
- Native Rust LLM integration (e.g. `llama.cpp`, `rustformers`)
- Local search engine (Tantivy)
- Native anti-injection firewall and OS integration

Phase 3 — Anvesha Ecosystem

- Local RAG indexing and vector store
- Native document search and encrypted on-device memory

Build instructions
------------------

1. Build Rust → WASM (from project root):

```bash
cd rust-wasm
wasm-pack build --target web --out-dir pkg --release
```

2. Copy `rust-wasm/pkg` output into the extension WASM folder:

```bash
cp -r rust-wasm/pkg/* extension/src/wasm/
```

3. Build the extension:

```bash
cd extension
npm install
npm run build
```

4. Load the extension in Chrome / Chromium:

```text
Open chrome://extensions
Enable Developer mode
Click “Load unpacked” → select `extension/dist/`
```

Notes
-----

- The repository is currently private while core architecture is developed. Contribution
  guidelines and a formal model will be published in Phase 2.
- Recommended license after Phase 1: MIT or Apache-2.0

Contact
-------

For questions about design or contribution during Phase 1, open an issue or reach
out to the maintainers listed in the project settings.





        
