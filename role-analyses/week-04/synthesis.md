# Workshop 4 Role Synthesis - RMS Access Control
## Santiago Vargas | October 15, 2026

**Role A:** Plant Cybersecurity Manager

**Role B:** Physical Security Officer

## Shared Evidence

This analysis concerns the authorized Radiation Monitoring System (RMS) course
simulation, not a production radiation detector or a verified plant layout. RMS is
logically Purdue Level 2, but its services and the SFPCM Level 1 role account share
one host. The HMI uses port 5060, the unauthenticated Modbus backend uses loopback
port 5061, and the replacement certificate-authenticated read-only gateway uses
loopback port 5062. Purdue labels are not enforced network or physical boundaries.

| Attack and chronology | Evidence-grounded result | Limit of the conclusion |
|---|---|---|
| A, October 14, after policy design | **Executable.** The legitimate `rms` account used backend 5061, device 1, FC6 at holding offset 3 (`40004`), to write 301 and restore 250. The comparison was `250 -> 300 -> 250`; the outside-band cycle was `250 -> 301 -> 250`. A separate read confirmed 250. | Backend point/function restrictions did not enforce the routine raw 200-300 policy band, role, or approval. The band is a simulation policy choice, not a physical safety limit. |
| B, supply chain | **Untestable under the current authorized scope. Not run and will not be run using the existing script.** No verified in-scope consumer for a permitted dependency/configuration manipulation and downstream consequence has been established. | No successful, blocked, or replacement experiment is claimed. Instructor acceptance of the limitation is not assumed. |
| C, original October 12 | **Executable before the written policy.** SFPCM reached the transparent `5062 -> 5061` relay and changed the threshold `250 -> 300 -> 250`; an independent read confirmed restoration. | This was not a test of an already-written policy. RMS write events and SIEM acknowledgements did not establish actor identity or authorization. |
| C, October 13 follow-up | **Blocked on the tested mTLS gateway path, port 5062.** The enrolled credential authenticated as `partner_read`, FC3 reads succeeded, FC6 returned `8601` (Illegal Function), and the threshold remained 250. | Backend 5061 remains a gateway bypass for callers able to reach it. Its isolation from SFPCM was not verified; A demonstrates backend writing as `rms`, not a new SFPCM-to-5061 test. |

Attack A's full source journal recorded four medium `protocol.write` events with
values `[300]`, `[250]`, `[301]`, and `[250]`, but null caller identity. Independently
retrieved SIEM records 67083-67086 showed the writes without populated target/value
fields, actor, or a distinguishing flag. A reviewer can identify 301 in the source
journal; the observed SIEM projection cannot distinguish it from the comparison
and restoration writes. This does not prove that every possible SIEM detector or
storage view lacks the information.

The existing `attack_b_supply_chain.py` stages a modified `events.py` that changes
an active service report to inactive and sends the false report through the event
pipeline. A test marker, temporary port, unchanged primary files, and a corrective
record do not make falsified SIEM telemetry permissible. Under the stated rules
of engagement (ROE), that action is forbidden. Static inspection supports this
scope decision, not a claim that any downstream system consumed the false event.
No alternative consumer or test is invented to fill the evidence gap.

## Plant Cybersecurity Manager

The manager asks three separate questions: who authenticated, what that identity
was authorized to do, and what evidence permits later review. An accepted SSH key
admits a caller to the shared `rms` account, not to one of seven enforced job roles.
The HMI's shared Basic-auth credential gates read-only routes, not named-person
permissions. The mTLS gateway improves credential authentication and read/no-write
authorization, but it does not restrict the backend maintenance path or implement
all seven human roles. Certificate possession is also not proof of exclusive human
key custody.

Attack A makes backend enforcement the immediate management issue: a legitimate
account could perform an outside-band change after the policy existed. Logging it
did not prevent it or prove approval. The manager should assign backend isolation
to the host administrator and role/range/approval enforcement to the RMS owner,
with evidence of effectiveness required before declaring either gap closed.
Maintaining source point/value details and correlating them with approvals is an
interim procedural measure, not an implemented automatic alarm or attribution
control. Gateway decisions currently have journal evidence, not demonstrated
follow-up SIEM ingestion.

For handover, the manager needs the exact permitted flows, named owners, SSH-key
fingerprint-to-person inventory, certificate allowlist and custody record, access
end dates, and approval/restoration records. The recorded client certificate expires
October 20, 2026 at 21:31 UTC; renewal or removal needs an assigned owner rather
than an assumption of permanent partner connectivity. Early revocation requires
allowlist removal and a gateway restart to terminate existing sessions. Neither
certificate enrollment nor a running service proves backend isolation.

## Physical Security Officer

The officer asks who can physically reach the equipment and its local interfaces:
the host or console, maintenance workstations, network connections, removable media,
and supporting power and environmental equipment. Entry permissions, escorts,
equipment custody, and tamper reporting would matter in a real deployment, but the
reviewed RMS records establish none of those physical arrangements. These are
verification and handover questions, not observed doors, badge readers, cabinets,
cable routes, or guards in this lab.

The SFPCM pivot does not demonstrate an intruder moving between rooms. It is a
logical shared-host path between role accounts over loopback. A Purdue Level 1-to-2
crossing does not establish physical adjacency or a protected-area crossing, and
there is no evidence that a predicted physical layout enabled or blocked this
attack. A locked room would not by itself prevent a remote, admitted account from
reaching another local service. Conversely, mTLS does not establish protection
against console access, equipment removal, or interruption of power.

For handover, the officer needs an actual equipment/location inventory and the
responsible access-control contact before asserting physical protection. If
physical-access records exist, preserve their original timestamps and correlate
them with host evidence without treating a badge entry as proof of a Modbus write.
The officer also needs clear escalation for suspected tampering or lost monitoring.
Raising the threshold or acknowledging an alarm is not a substitute for verifying
conditions, and simulated readings cannot establish real radiation conditions.

## Divergence Analysis

Both roles reject the assumption that admission grants unrestricted authority, but
their primary boundaries differ. The manager prioritizes authentication,
operation-specific authorization, audit fidelity, and the backend bypass. The
officer prioritizes physical reachability, custody, supervised maintenance, and
access to local interfaces. A valid certificate can satisfy a cyber admission check
without granting a write; a valid badge can satisfy an entry check without granting
process-control authority. Neither credential alone proves who changed a threshold.

Their containment choices can diverge. Removing a gateway certificate addresses
one logical path but leaves backend access and possible physical access unchanged.
Restricting room entry addresses physical reachability but does not revoke an
already-admitted remote account. Shutting down the host could remove monitoring
needed by both roles. Joint decisions therefore need supervisor/system-owner
coordination, preserved evidence, and a plan to maintain monitoring rather than an
unqualified instruction to disconnect or power off equipment.

## Synthesis and Handover

The joint decision is to hand over partial remediation with explicit accepted gaps,
not to label RMS fully protected. The primary RUNBOOK and Purdue annotation now
document the operational baseline, tested paths, actual HMI screenshot, and gaps.
The original architecture page is still unavailable for independent review; its
RMS link table is preserved in the W3 brief. The handover must expose this evidence
limitation rather than imply that every rubric item or control has been verified.

- Record the tested topology: HMI 5060, read-only mTLS gateway 5062, backend 5061, and the shared-host bypass risk. Keep intended DCS telemetry relationships separate from demonstrated SFPCM tests.
- Use the RUNBOOK's start/stop and health-check instructions for `plant-rms`, `plant-rms-hmi`, and `plant-rms-relay`, including authorized maintenance ownership and post-change monitoring checks. October 15 read-only checks found all active, threshold 250, and HMI authentication working; stop/start procedures were not exercised that day.
- Carry forward all eight points from W3 `points.md`, their scaling and zero-based offsets, and the RUNBOOK's additional source-only discrete-input finding. Normal threshold raw 250 means 2.50 uSv/h; `40004` changes the alarm comparison, not the radiation measurement. Coil `00001` is acknowledgement, not permission to suppress alarms.
- Preserve A's client output, full source events, SIEM records, C's original and follow-up transcripts, gateway decisions, approval records, and UTC/MDT correlation. Distinguish receipt, detection, authorization, and person-level attribution.
- Carry forward A as Executable, C as Executable October 12 and Blocked only on the October 13 gateway path, and B as Untestable under current scope. Do not execute the telemetry-falsification script or present its existence or local tests as a live result.
- Assign closure owners for backend isolation, role/range enforcement, audit-value visibility, credential lifecycle, and physical-inventory verification. Until verified, retain these as gaps rather than silently promoting policy requirements to controls.
- On an unexpected threshold or loss of visibility, preserve the observed state and relevant records, notify the supervisor, RMS owner, and cybersecurity manager, and involve the physical security contact if tampering is suspected. Do not erase logs, fabricate telemetry, or make unapproved threshold changes to hide the symptom.

Cyber and physical access controls are complementary, not interchangeable. The
strongest shared conclusion is narrowly evidenced: the gateway denied a specific
authenticated write, the backend still allowed legitimate-account misuse, and no
physical layout or compliant supply-chain execution has been demonstrated.

## Evidence References

Paths below are relative to the sibling `primary` repository.

- `workshops/week-04/README.md`: required role pairing and handover deliverables.
- `workshops/week-04/rbac-policy.md`: seven policy roles, actual mechanisms, routine band, gateway boundary, and accepted enforcement gaps.
- `workshops/week-04/adversary-test.md`: A evidence summary, B Untestable disposition, original C and path-specific follow-up.
- `workshops/week-04/session-log.md`, Sessions 3, 5, 7, 9, and 10: chronology, credential limits, live results, and handover status.
- `workshops/week-04/adversary-test.md`, embedded Attack A Evidence: source values, restoration, and independent SIEM records 67083-67086.
- `workshops/week-03/lab/attack_b_supply_chain.py`, especially `staged_dependency()` and `main()`: static evidence of the forbidden false service-state telemetry design; not executed for this synthesis.
- `workshops/week-03/points.md`: eight points, scaling, process behavior, and simulation limitations.
- `workshops/week-04/RUNBOOK.md` and `purdue-annotated-description.md`: operational handover, topology annotation, actual mechanisms, screenshot, and evidence limitations.
- `workshops/week-04/session-log.md`, October 15 Collection: read-only service/HMI checks and 31 passing local tests; no new attack execution.

The secondary README was empty and its Week 04 directory contained no synthesis
template at review time. This document uses the established secondary role-analysis
structure and the primary Week 04 role requirement. ROE constraints and the current
Attack B Untestable disposition follow the October 15 scope review. The synthesis
itself was drafted from local records; the separate October 15 collection records
the primary work's read-only live checks. No new attack execution is claimed.

## October 18 Review Status

Codex reviewed this synthesis against the primary evidence and the supplied
assignment. Its conclusions remain unchanged: A was Executable, C's later denial
applies only to the tested gateway path, and B remains Untestable. The primary
Week 04 README now indexes the deliverables and identifies the missing original
architecture review, unresolved B execution/acceptance, and required author review.
These are submission limits as well as handover limits. Neither role should sign
off on them as verified controls or completed experiments. No new partner contact,
physical inspection, live attack, or personal author approval is claimed here.
