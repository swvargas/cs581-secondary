# Role Analysis, Workshop 2
## Santiago Vargas | RMS

**Role A:** Nation-State Threat Analyst  
**Role B:** Insider Threat Investigator

## Nation-State Threat Analyst

The nation-state threat analyst would use my TEMP.Veles profile and cards to prioritize documented capabilities around the radiation monitoring system (RMS). TEMP.Veles leads because reporting ties it to TRITON's compromise of industrial safety controllers. Valid accounts, RDP jump boxes, PowerShell, lateral tool transfer, program downloads, unauthorized commands, and indicator removal form a technical sequence to hunt. The analyst would seek unexpected remote sessions, host-to-host transfers, scripts, program changes, and disagreement between RMS indications and historian or PPC records. Sandworm's unauthorized commands and Dragonfly's compromised software add command-integrity and supply-chain hypotheses. CyberAv3ngers adds default-credential exposure; DarkSide shows that IT compromise can interrupt operations without demonstrated OT access.

The analyst would not claim these actors targeted this RMS. My profile finds no public evidence of TEMP.Veles nuclear or RMS targeting, every card calls its RMS connection theoretical, and the Week 1 map establishes no reverse path from ICT-SIEM. The first action is therefore to verify the architecture and collect evidence at the Level 3/4 firewall, log collector, OT sensor, and any historian or PPC feed. Attribution remains assessed: TEMP.Veles, XENOTIME, TsNIIKhM, and all TRITON operators are not proven identical.

## Insider Threat Investigator

The insider threat investigator would begin with the Maroochy Water Breach Insider card without turning one grievance-driven case into a personality profile. The card documents a former contractor using system knowledge and radio equipment to send false data and commands. For RMS, that supports checking who retains maintenance knowledge, portable equipment, accounts, and access after role or contract changes—not assuming that a disgruntled insider or Maroochy-style radio path exists.

Anderson's **security-usability** concept changes what counts as a cause. Chapter 3 explains that difficult security and unsafe defaults invite failure; “careless users” are not a sufficient explanation. Relevant conditions include shared or default credentials, excessive privileges, awkward maintenance, weak offboarding, and pressure that rewards bypasses. They can enable misuse or error but do not prove intent.

Anderson's **password reuse and credential stuffing** (Section 3.4.9.2) limits the meaning of a valid-account alert. An unusual successful login may reflect a stolen reused password, TEMP.Veles, or an insider. The observable evidence is the account, source, time, device, privilege, failures, and later commands—not motive. The investigator would correlate these facts with approved work, role changes, access reviews, and independent RMS indications.

Anderson's **deception and password-canary** concept (Section 3.4.9.2) offers a stronger indicator. Use of a monitored decoy credential that no legitimate workflow needs is directly observable and more discriminating than dissatisfaction. Approved honeytokens could reveal credential searching or misuse, subject to nuclear configuration and safety review. Even then, the alert proves use of the token, not the person's motive.

## Divergence and Synthesis

Both roles read the same reporting but act differently. The threat analyst starts with historical TTPs and asks where TEMP.Veles-like activity would appear. The investigator starts with organizational conditions and separates observable behavior from inconvenience, error, theft, and malice. A valid account prompts the analyst to hunt for RDP and lateral movement; it prompts the investigator to verify ownership, offboarding, work context, reuse, and theft.

Together, they support one defensible action: verify RMS architecture; baseline authorized accounts, maintenance paths, and program changes; correlate network, host, authentication, and independent process evidence; and investigate without assigning motive early. The nation-state lens supplies technical hypotheses; the insider lens reduces false accusation and exposes enabling conditions. Neither turns Week 1's inferred interfaces or the cards' theoretical RMS relevance into facts.

## Sources

- Ross Anderson, *Security Engineering*, 3rd ed., Chapter 3, “Psychology and Usability,” especially Sections 3.4.9.2 and 3.6.
- MITRE ATT&CK, TEMP.Veles (G0088) and Triton Safety Instrumented System Attack (C0030), as cited in my Workshop 2 adversary profile.
- CISA, FBI, and DOE, AA22-083A, *Tactics, Techniques, and Procedures of Indicted State-Sponsored Russian Cyber Actors Targeting the Energy Sector*, as cited in my Workshop 2 profile.
- Marshall Abrams, *Malicious Control System Cyber Security Attack Case Study: Maroochy Water Services, Australia* (2008), as cited in threat card 5.
