<p align="center">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 140" width="100%">
    <style>
      .bg { fill: #080a0d; rx: 12px; stroke: rgba(255,255,255,0.1); stroke-width: 1px; }
      .text {
        font-family: 'Courier New', Courier, monospace;
        font-size: 38px;
        font-weight: 800;
        fill: #79eaff;
        animation: glow 3s ease-in-out infinite alternate;
      }
      .subtext {
        font-family: system-ui, -apple-system, sans-serif;
        font-size: 16px;
        fill: #f5f7fb;
        opacity: 0.6;
      }
      .cursor {
        fill: #d36aff;
        animation: blink 1s step-end infinite;
      }
      .line {
        stroke: #a7ffd7;
        stroke-width: 2;
        stroke-dasharray: 1000;
        stroke-dashoffset: 1000;
        animation: draw 4s ease forwards;
      }
      @keyframes blink { 50% { opacity: 0; } }
      @keyframes glow {
        from { filter: drop-shadow(0 0 2px rgba(121, 234, 255, 0.4)); }
        to { filter: drop-shadow(0 0 12px rgba(121, 234, 255, 0.8)) drop-shadow(0 0 24px rgba(211, 106, 255, 0.4)); }
      }
      @keyframes draw { to { stroke-dashoffset: 0; } }
    </style>
    <rect width="100%" height="100%" class="bg"/>
    <text x="40" y="75" class="text">Text Compactor</text>
    <rect x="365" y="45" width="20" height="38" class="cursor"/>
    <text x="40" y="105" class="subtext">Zero-loss semantic compression. Same meaning, tighter form, no drift.</text>
    <path d="M 40 120 L 760 120" class="line"/>
  </svg>
</p>

**Text Compactor** is a serverless, client-side web application designed for forensic semantic compression. Unlike standard AI summarizers that hallucinate or drop crucial facts, Text Compactor tightly edits prose while mathematically guaranteeing the preservation of original meaning. 

Users bring their own API keys to strip filler, repetition, and dead phrasing across four distinct tonal styles. Its standout feature is an automated **Preservation Audit** pipeline that extracts high-value tokens before compression, verifies their existence in the output, and automatically triggers a repair sequence if data is lost. Packaged in a single HTML file, it requires no backend and executes entirely in the browser.

---

### Intent

Generative AI is notoriously bad at precision editing. It prefers to summarize, rewrite entirely, or hallucinate new framing. The intent behind Text Compactor is to force LLMs into a strict "Forensic Editor" role. It acts as a precision scalpel that removes linguistic fat while proving via its regex audit system that it has not accidentally amputated vital facts, figures, or exact quotes.

### Primary Use Cases

*   **Professional Writers:** Tightening bloated articles or manuscripts to meet strict word counts without altering the author's core thesis.
*   **Corporate Communications:** Condensing lengthy memos into punchy formats while ensuring critical compliance acronyms (e.g., HIPAA, ADA) are strictly retained.
*   **Prompt Engineering (Meta-Use):** Compressing verbose user prompts or context windows before sending them down an AI pipeline, saving on API token costs without losing data fidelity.

---

### Technical Architecture

*   **Single-File Deployment:** Entirely contained in `index.html`. Zero build steps. Zero backend dependencies.
*   **Verified Models:** Configured for the latest API standards including OpenAI `gpt-5.5`, Anthropic `claude-sonnet-4-5`, and DeepSeek `deepseek-v4-pro`.
*   **BYOK (Bring Your Own Key):** Credentials remain strictly in local browser session storage.
*   **Preservation Audit Engine:** Pre-execution regex extraction flags dates, currencies, quotes, and specialized acronyms to ensure absolute retention.
```eof
