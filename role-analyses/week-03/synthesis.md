# Workshop 3 Role Synthesis — ICS/SCADA Engineer vs. General Counsel

## Shared Evidence

The RMS lab exposes a changing radiation process through traditional Modbus/TCP on
loopback, an HTTPS HMI protected by Basic authentication, SSH-tunneled remote access,
and self-reported OT-SIEM events. My capture shows cleartext Modbus function-code 3
requests and raw values. The source permits two operational writes but Modbus supplies
no client identity or authorization field. The live services are enabled and survived
logout, unauthenticated HMI requests returned 401, and the SIEM accepted some events
while other delivery attempts timed out.

**Confidence: documented. Provenance:** W3 `capture.pcap`, live service checks,
`points.md`, and `lab/`, October 5, 2026.

## ICS/SCADA Engineer

The engineer asks whether the process remains observable and safe when components
fail. Loopback binding and SSH tunneling reduce exposure, but one bind setting is not
defense in depth. The engineer would define exact allowed data flows, add point- and
range-aware filtering, validate every request, monitor protocol behavior independently,
and test failure modes such as lost SIEM connectivity, stale data, an unavailable HMI,
malformed requests, and conflicting threshold changes. Changes must respect process
availability and maintenance windows; a security control that delays or blocks required
alarm data can create its own hazard.

The engineer also treats the low threshold found in the capture as a configuration-
management problem. The packet proves the value but not who changed it or why. A
production system should record old and new values, named identity, approval, device
result, and independent confirmation. Redundant indication and fail-safe limits matter
more than merely adding encryption.

**Confidence: assessed.** These are engineering conclusions derived from the lab;
they are not verified characteristics of a real nuclear RMS.

## General Counsel

Counsel asks different questions of the same facts: Which systems and records are in
regulatory scope? Who had a duty to protect them? What did the organization know,
when did it know it, and what evidence can it preserve? A shared `rms` account, Basic
authentication, indefinite SSH keys, and self-asserted SIEM events complicate proof.
An SSH fingerprint may permit later attribution only if the organization maintained a
reliable fingerprint-to-person record. A Modbus write and an RMS-generated alert do
not by themselves establish a particular actor, malicious intent, or complete event
history.

Counsel would preserve the packet capture, systemd journal, authentication records,
authorized-key history, SIEM acceptance and failure logs, configuration baselines,
work orders, and chain of custody. Counsel should not claim that the three analyzed
CVEs affect this lab: they concern named commercial products, while this build uses
`pymodbus`. Nor should counsel convert NIST guidance or a course Purdue level into a
facility-specific legal obligation without determining jurisdiction, system scope,
license conditions, contracts, and reportability facts.

**Confidence: assessed.** The evidentiary issues follow from the observed design;
specific legal duties remain unknown without facility and jurisdiction facts. This is
technical-academic analysis, not legal advice.

## Divergence and Joint Decision

The engineer prioritizes safe availability, deterministic behavior, and changes that
do not interrupt operations. Counsel prioritizes defensible scope, preservation,
attribution, notification decisions, and language that does not outrun the evidence.
Their immediate recommendations can therefore diverge. Counsel may favor rapid
isolation to contain exposure and preserve evidence, while the engineer may oppose
disconnecting a monitoring path until an alternate indication is operating. Continued
operation can protect process awareness while changing volatile evidence or extending
network exposure; isolation can protect evidence while reducing operational visibility.

A decision satisfying both roles would establish an incident runbook before the event.
It would name decision owners, define safety-preserving containment options, synchronize
and protect logs, map SSH fingerprints to individuals, record approvals for every
control write, preserve packet and host evidence, and specify escalation criteria for
regulatory and contractual review. Controls would be tested during an approved window,
including SIEM outage and recovery, rather than accepted because a policy says they
exist.

## Synthesis

The capture gives both roles the same central lesson: network data can prove that a
Modbus operation and value crossed an observation point, but it cannot prove identity,
authorization, intent, physical truth, or legal consequence. The engineer closes that
gap with architecture, validation, redundancy, and testing. Counsel closes it with
scope decisions, attributable records, preservation, and disciplined claims. The best
control produces evidence useful to both without degrading the plant function it is
supposed to protect.

## Sources

- Modbus Organization, [Modbus Application Protocol Specification V1.1b3](https://www.modbus.org/file/secure/modbusprotocolspecification.pdf).
- Modbus Organization, [Modbus/TCP Security Protocol v3.6](https://www.modbus.org/docs/MB-TCP-Security-v36_2021-07-30.pdf).
- NIST, [SP 800-82 Rev. 3, Guide to Operational Technology Security](https://doi.org/10.6028/NIST.SP.800-82r3), 2023.
- NVD CVE API records for CVE-2018-7857, CVE-2024-11737, and CVE-2025-55221, retrieved October 5, 2026.
