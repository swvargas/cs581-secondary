# Role Analysis, Workshop 1
## Santiago Vargas | ICT-SIEM

**Role A:** NRC Regulator

**Role B:** Plant Cybersecurity Manager

## NRC Regulator Perspective

An NRC regulator would first question the scope of my attack-surface map. The course architecture places ICT-SIEM at Corporate Level 4, but that does not prove it is covered by the licensee's cyber security program. Under 10 CFR 73.54(a), the licensee must protect digital systems and networks associated with safety, security, and emergency preparedness functions, including support systems that could adversely affect those functions. The regulator would ask for the licensee's documented scope and Critical Digital Asset determination before treating an ICT-SIEM control as a regulatory requirement. RG 5.71 Section 3.1 provides guidance for identifying these assets, but the regulation defines the required scope.

If ICT-SIEM is in scope, the regulator would focus on whether its monitoring data can be trusted. My map identifies possible failures involving event collection, time synchronization, storage, identity services, boundary devices, and analyst access. RG 5.71 Appendix B Sections B.2.2 through B.2.9 address audit generation, review, storage capacity, time stamps, and protection of audit information. The regulator would ask for architecture diagrams, configuration baselines, access records, alert tests, time synchronization evidence, retention settings, and corrective-action records. A data diode, LDAP connection, REST API, or physical-security feed should not be accepted as fact without facility evidence.

The manipulated OT-SIEM export scenario would raise questions about the licensee's ability to detect, respond to, and recover from a cyberattack under 10 CFR 73.54(c). A failed monitoring feed may indicate ineffective audit protection, transmission integrity, or defense in depth. It does not automatically prove a reportable event. The regulator would still need to determine program scope, effects on an SSEP function, discovery time, and whether the criteria in 10 CFR 73.77 were met.

## Plant Cybersecurity Manager Perspective

The plant cybersecurity manager would turn those questions into operational tasks. The first action would be to compare the public map with the approved facility architecture and asset inventory. This would confirm whether OT-SIEM exports to ICT-SIEM, which boundary device controls the path, whether a return route exists, and who owns the collector, time source, database, analyst workstations, and escalation process.

The manager would then test the full monitoring chain. A known event could be generated at an approved source and followed through collection, boundary transfer, storage, correlation, and analyst notification. The test should compare time stamps and measure delay or loss. It should also check parser failures, duplicate events, storage exhaustion, queue backup, disabled agents, expired certificates, and excessive service-account privileges. NIST SP 800-82 Rev. 3 Sections 5.2.3.1 and 5.2.3.3 support segmentation and monitoring, while Appendix E.2.1 discusses centralized log collection and SIEM use. These sources support the control goals, but only facility testing can verify the implementation.

The manager also has to work within outage schedules, vendor support, configuration control, and safety review. If a legacy product cannot support the preferred protection, the manager may need a documented compensating control and a plan to test it. The control should not be treated as effective only because it appears in a procedure.

## Divergence Analysis

The regulator and manager use the same evidence for different decisions. The regulator decides whether the licensee meets requirements and can prove that controls are effective. The manager decides what can be changed safely, who performs the work, and how monitoring continues during maintenance. An unverified one-way export is an inspection evidence gap for the regulator. For the manager, it becomes a task to identify the hardware, test directionality, preserve service, and correct either the documentation or configuration.

## Synthesis

A decision that satisfies both roles would document whether ICT-SIEM is in scope, confirm the real data path, test monitoring integrity and availability, record the evidence, and assign corrective actions with owners and dates. My database background helps identify missing events, bad time stamps, parser errors, duplicate records, and storage limits. The regulatory lens adds scope and proof. The management lens adds ownership, testing, and safe implementation. Together they turn a public attack-surface map into questions a licensee could verify and act on.

## Sources

- [10 CFR 73.54, Protection of Digital Computer and Communication Systems and Networks](https://www.ecfr.gov/current/title-10/chapter-I/part-73/section-73.54)
- [10 CFR 73.77, Cyber Security Event Notifications](https://www.ecfr.gov/current/title-10/chapter-I/part-73/section-73.77)
- [NRC Regulatory Guide 5.71, Cyber Security Programs for Nuclear Facilities](https://scp.nrc.gov/slo/regguide571.pdf), Section 3.1 and Appendices A, B, and C, 2010
- [NIST SP 800-82 Rev. 3, Guide to Operational Technology Security](https://doi.org/10.6028/NIST.SP.800-82r3), Sections 5.2.3.1, 5.2.3.3, and Appendix E.2.1, 2023
