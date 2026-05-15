# TEXT COMPACTOR



Text Compactor is a serverless, client-side web application designed for forensic semantic compression. Unlike standard AI summarizers that hallucinate or drop crucial facts, Text Compactor tightly edits prose while mathematically guaranteeing the preservation of original meaning.



Users bring their own API keys to strip filler, repetition, and dead phrasing across four distinct tonal styles. Packaged in a single HTML file, it requires no backend and executes entirely in the browser.



### THE AUDIT ENGINE



The defining technical feature of this application is the **Preservation Audit**. Generative AI is notoriously bad at precision editing; it prefers to summarize or rewrite entirely. 



To solve this, Text Compactor forces the LLM into a strict "Forensic Editor" role. Before any API request is sent, a pre-execution regex engine extracts high-value tokens from the user's text. 
```yaml
Protected_Entities:

  - Exact Quotes ("...")

  - Financial Metrics ($5,000.00)

  - Dates (04/12/2026, Nov 15th)

  - Percentages and Timeframes (15%, 45 days)

  - Compliance Acronyms (HIPAA, ADA, OSHA)
```
Post-execution, the engine verifies the existence of these exact tokens in the output. If the LLM amputated a vital fact, the system detects the discrepancy and automatically triggers a secondary repair prompt to restore the missing data.
```
Diff

- DRAFT: The patient was seen for compliance checks.+ VERIFIED: The patient was seen on 04/12/2026 for ADA compliance checks.
```
PRIMARY USE CASES

Professional Writers: Tightening bloated articles or manuscripts to meet strict word counts without altering the author's core thesis.

Corporate Communications: Condensing lengthy memos into punchy formats while ensuring critical compliance acronyms and financial metrics are strictly retained.

Prompt Engineering (Meta-Use): Compressing verbose user prompts or context windows before sending them down an AI pipeline, saving on API token costs without losing data fidelity.

TECHNICAL ARCHITECTURE

Single-File Deployment: Entirely contained in index.html. Zero build steps. Zero backend dependencies.

BYOK (Bring Your Own Key): Credentials remain strictly in local browser session storage (sessionStorage). Keys are never sent to a third-party server, only directly to the selected provider.

Zero-Dependency UI: Built completely with vanilla CSS variables, Grid/Flexbox layouts, and semantic HTML. No React, no Tailwind, no NPM.
