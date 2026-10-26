# Workshop 5: Two Inspectors, One Evidence Ledger
Santiago Vargas | EDGC | October 26, 2026

## Shared Facts

This is the authorized CS 581 simulation, analyzed as a covered US power-reactor incident subject to confirmation of actual license assumptions. The primary analysis is `workshops/week-05/three-framework-analysis.json` in `swvargas/cs581-primary`; preserved `siem-*-high.json` responses and `evidence-notes.md` supply the evidence, not the previous RMS workshop tests.

EDGC **116181** reports forced-normal standby-power status with a persistent fault at **2026-10-22T04:45:00Z**. Cross-system DCS **116173** places first observed control-data divergence at **October 9, 08:47 UTC**; DCS **116182** dates supervisor discovery to **October 23, 08:47 UTC**. RMS **116180**, October 20 at 02:59, reports accounting/instrument alteration; SFPCM **116177**, October 14 at 07:40, reports a divergent level display. SMR **116172**, October 9 at 07:24, is earlier possible reconnaissance. These are direct SIEM retrievals, not owner-confirmed Canvas posts. Neither writes nor read aggregates establish a person's identity. The scenario stipulates one campaign/actor; the snapshots do not independently prove that attribution.

## NRC Security Inspector

The NRC inspector asks whether the licensee protected covered digital assets and promptly recognized, contained and reported compromise of safety, security and emergency-preparedness functions. EDGC's masked status makes accurate functional monitoring and escalation central. The inspector would request source journals, credential issuance/revocation and custody records, digital-asset scope, incident recognition logs, compensatory measures, report receipts and clean-recovery tests. A legitimate credential is not proof of legitimate use or a named insider; the missing PSI record must be obtained rather than inferred.

Timing comes from **10 CFR 73.77**, not merely the protective-program requirements of 73.54: adverse covered functional impact requires notification within **one hour after discovery**, potential impact within **four hours**, and reconnaissance information has its distinct **eight-hour** category. A fourteen-day-old divergence is evidence of dwell time, not automatically a fourteen-day-old discovery. If qualifying discovery occurred at the October 23 supervisor observation, the one-hour deadline was 09:47 UTC; whether recognition occurred then or earlier remains unconfirmed. Security resolution requires verified containment, credential correction, trustworthy configurations and indications, persistence investigation and corrective actions, not just a normal status bit or a completed report.

## IAEA Safeguards Inspector

The IAEA inspector asks whether declared nuclear material remains accounted for and whether continuity of knowledge survives the campaign. RMS record alteration matters because trusted accounting, measurements and surveillance may disagree. The inspector would seek independent instrument records, material-balance and transaction histories, physical inventory, seal and surveillance continuity, and facility-specific safeguards arrangements. EDGC masking may affect trust in supporting infrastructure, but is not itself evidence that nuclear material moved.

The inspector's authority is not interchangeable with the NRC cyber inspector's. US facility eligibility alone does not establish that **75.36** special reporting applies; obtain the **75.7(a)** designation or other applicable agreement status and license conditions. For covered entities, 75.36(b) requires an **immediate telephone report to NRC** for specified loss, containment change permitting removal, or license-condition triggers. NRC transmits specified Part 75 information to IAEA under **75.13(a)**. Separately, domestic **74.11(a)** requires an NRC report within **one hour of discovery** of covered SNM loss, theft, diversion or attempt. Altered records alone do not prove those facts. No generic direct-to-IAEA one-hour or twenty-four-hour deadline is established here.

## Coordination And Disagreement

Both inspectors need the same preserved, timestamped ledger, but each tests a different proposition. Security containment can succeed while a material discrepancy remains unresolved; physical reconciliation can succeed while malicious persistence remains. Isolation that breaks surveillance or an unrecorded database restore could improve cyber posture while worsening safeguards continuity. The coordinator must preserve originals, record compensatory observations and approve recovery with operations and the material custodian, not let one inspector's closure substitute for the other's.

The practical handoff is DCS/SMR recognition chronology to the security reporting owner, EDGC/RPS/SFPCM functional assessments to shift engineering, and RMS/PSI records plus physical reconciliation to the material custodian. No owner confirmations or Canvas participation are fabricated: local `canvas-handoff-draft.md` is **not posted**, PSI/RPS historic incident evidence was unavailable in capped windows, and Part 75 designation is unknown. A shared NRC call can avoid specified Safety/Security duplication under 73.77(c)(7) only if it names both criteria and meets the earliest deadline; it does not automatically discharge material obligations.

Neither inspector's mandate alone answers the remaining plant-wide question: what independent evidence establishes simultaneously that the process is safe, unauthorized access is gone, and all material remains accounted for?

## Live Sources

Retrieved October 26, 2026 via `webfetch` and delegated live government eCFR research; required MCP reader was unavailable. NRC-hosted CFR pages returned 403. eCFR was labeled up to date through October 22; primary `regulatory-sources.md` records retrieval details and qualifications.

- [10 CFR 73.77](https://www.ecfr.gov/current/title-10/section-73.77): cyber notification, corrective-action recording and written followup.
- [10 CFR 74.11](https://www.ecfr.gov/current/title-10/section-74.11): domestic SNM loss/theft/diversion/attempt reporting.
- [10 CFR 75.36](https://www.ecfr.gov/current/title-10/section-75.36): applicable safeguards special reports.
- [Part 75, including 75.7](https://www.ecfr.gov/current/title-10/chapter-I/part-75) and [75.13](https://www.ecfr.gov/current/title-10/section-75.13): designation and NRC-to-IAEA information transmission.
