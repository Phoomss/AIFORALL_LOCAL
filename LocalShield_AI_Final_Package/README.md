# LocalShield AI — Final Review Package

This folder contains a revised concept proposal, a 10-slide HTML pitch, and an interactive HTML prototype.

## Files

- `LocalShield_AI_Final_Proposal.md` — detailed idea proposal, technical architecture, MVP boundaries, KPI definitions, team roles and evidence ledger.
- `LocalShield_AI_Final_Presentation.html` — 10-slide self-contained HTML presentation with an embedded synthetic demo and a team slide.
- `LocalShield_AI_Prototype.html` — standalone interactive web prototype.
- `Submission_Readiness_Checklist.md` — critical event-rule checks and remaining actions.
- `QA_Report.md` — static validation status and tests not completed.

## How to use

1. Open `LocalShield_AI_Final_Presentation.html` in Chrome or Edge.
2. Navigate with Previous/Next or the left/right arrow keys. Press `F` for fullscreen.
3. On the interactive demo slide, calculate the plan, close road B–D, recalculate, approve, then reset.
4. Open `LocalShield_AI_Prototype.html` for the enhanced standalone prototype featuring:
   - **Visual Plan Diff Viewer:** Side-by-side v1 vs v2 comparison with delta metrics and AI explanations
   - **Vehicle Clearance Filter:** Dynamic routing for Motorcycle (<15cm), 4WD Truck (<45cm), and Rescue Boat (>30cm water transit)
   - **AI Multimodal SOS Intake:** LINE chat, Voice Memo with audio waveform, and photo alerts with automated PDPA masking and vulnerability triage
   - **4-Role Persona Switcher:** Coordinator, Local SME Merchant with Digital Escrow Payout, Volunteer Driver with mobile dispatch & proof-of-delivery, and Resident SOS Tracker
   - **Automated SitRep Export:** Instant Situation Report generation in Markdown and Print/PDF layout
5. Use the Markdown proposal as a content source; edit event-specific sections only after confirming the target competition's official brief.

## Important scope and evidence notes

- All demo data and computed KPI values are synthetic.
- The HTML prototype uses local JavaScript logic; it does not call a live LLM, flood API, road API, database, AWS service or Amazon QuickSight.
- The full system architecture is proposed, not deployed.
- The five-member team information is included as supplied, but some events limit teams to 3–4 people. Confirm the applicable rules before submitting.
- If this is for Sea x OpenAI Regional Codex Hackathon Thailand, its published event page lists three build directions and a 3–4 member team limit. It also states that new building must occur on event day and pre-built code/existing projects shall not be submitted. See `Submission_Readiness_Checklist.md` before using any prebuilt file for that event.
