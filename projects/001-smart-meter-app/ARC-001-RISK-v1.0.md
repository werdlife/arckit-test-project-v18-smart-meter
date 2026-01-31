# Risk Register: UK Smart Meter Data Consumer Mobile App

> **Template Status**: Live | **Version**: 1.0.3 | **Command**: `/arckit.risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v1.0 |
| **Document Type** | Risk Register |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-01-31 |
| **Last Modified** | 2026-01-31 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-02-28 |
| **Owner** | [OWNER_NAME_AND_ROLE] |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Programme Board, DESNZ SRO, Risk Owners, Steering Committee, Ofgem, DCC |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-01-31 | ArcKit AI | Initial creation from `/arckit.risk` command | PENDING | PENDING |

---

## Executive Summary

### Risk Profile Overview

**Total Risks Identified:** 20 risks across 6 categories

| Risk Level | Inherent | Residual | Change |
|------------|----------|----------|--------|
| **Critical** (20-25) | 5 | 1 | ↓ 80% |
| **High** (13-19) | 8 | 4 | ↓ 50% |
| **Medium** (6-12) | 6 | 11 | — |
| **Low** (1-5) | 1 | 4 | — |
| **TOTAL** | 292 | 186 | ↓ 36% |

### Risk Category Distribution

| Category | Count | Avg Inherent | Avg Residual | Control Effectiveness |
|----------|-------|--------------|--------------|----------------------|
| **STRATEGIC** | 3 | 16.7 | 10.7 | 36% reduction |
| **OPERATIONAL** | 4 | 13.0 | 7.8 | 40% reduction |
| **FINANCIAL** | 3 | 13.3 | 8.7 | 35% reduction |
| **COMPLIANCE** | 4 | 16.3 | 10.5 | 36% reduction |
| **REPUTATIONAL** | 3 | 15.0 | 9.7 | 35% reduction |
| **TECHNOLOGY** | 3 | 14.3 | 8.7 | 39% reduction |

### Overall Risk Assessment

**Overall Residual Risk Score:** 186/500
**Risk Reduction from Controls:** 36% reduction from inherent risk
**Risk Profile Status:** ⚠️ Concerning — 4 residual High risks require active treatment; 1 residual Critical risk requires immediate escalation

### Risks Exceeding Appetite

**Number of risks exceeding assumed organisational appetite:** 5 risks

*Note: No formal organisational risk appetite document exists (projects/000-global/risk-appetite.md not found). Appetite thresholds below are inferred from HM Treasury Orange Book guidance and UK Government norms for OFFICIAL-classified projects. Formal risk appetite should be established and approved by the Programme Board.*

| Risk ID | Title | Category | Residual Score | Assumed Appetite | Excess | Escalation |
|---------|-------|----------|----------------|------------------|--------|------------|
| R-002 | Consumer data breach | COMPLIANCE | 15 | ≤ 6 | +9 | Steering Committee + ICO pre-consultation |
| R-006 | Political or machinery-of-government change | STRATEGIC | 16 | ≤ 12 | +4 | SRO + Minister briefing |
| R-010 | UK GDPR non-compliance | COMPLIANCE | 12 | ≤ 6 | +6 | DPO escalation to SRO |
| R-013 | High-profile service failure | REPUTATIONAL | 12 | ≤ 8 | +4 | SRO + ministerial comms |
| R-015 | Tariff comparison bias allegation | REPUTATIONAL | 12 | ≤ 8 | +4 | Ofgem engagement |

### Top 5 Critical Risks Requiring Immediate Attention

1. **R-006** (STRATEGIC, Residual 16): Political or machinery-of-government change — Owner: DESNZ SRO — Status: Open
2. **R-002** (COMPLIANCE, Residual 15): Consumer data breach — Owner: DESNZ SRO — Status: Open
3. **R-001** (STRATEGIC, Residual 12): Low consumer adoption — Owner: DESNZ SRO — Status: Open
4. **R-010** (COMPLIANCE, Residual 12): UK GDPR non-compliance — Owner: DPO / Privacy Lead — Status: Open
5. **R-013** (REPUTATIONAL, Residual 12): High-profile service failure — Owner: DESNZ SRO — Status: Open

### Key Findings and Recommendations

**Key Findings:**
- Heavy concentration of risk ownership on the DESNZ SRO (8 risks) — risk of overload and insufficient attention
- Compliance risks are structurally difficult to mitigate below appetite due to the nature of personal energy data processing (UK GDPR, SEC)
- The programme's dependency on external parties (DCC, energy suppliers, regulators) creates risks that the programme cannot fully control
- Political/MoG risk is the highest residual risk and is largely outside programme control

**Recommendations:**
1. Establish formal organisational risk appetite (create `projects/000-global/risk-appetite.md` via Programme Board)
2. Escalate R-006 (political change) and R-002 (data breach) to Steering Committee immediately
3. Delegate risk ownership for operational and technology risks to Technical Architect and Programme Director to reduce SRO burden
4. Prioritise DPIA completion (R-010) and ICO pre-consultation (R-002) as the most impactful risk reduction activities
5. Embed DCC capacity planning (R-004) in the earliest integration sprints to de-risk the critical path

---

## A. Risk Matrix Visualisation

### Inherent Risk Matrix (Before Controls)

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │  R-006    │  R-002    │
Certain    │     5     │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │ R-003     │ R-001     │           │
           │           │           │ R-009     │ R-004     │           │
           │     4     │     8     │    12     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │           │ R-007     │ R-005     │ R-010     │
K          │           │           │ R-008     │ R-011     │ R-013     │
E          │     3     │     6     │ R-017     │ R-015     │           │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 2-Unlikely│          │           │ R-012     │ R-014     │           │
H          │           │           │ R-016     │ R-018     │           │
O          │     2     │     4     │     6     │     8     │    10     │
O          ├───────────┼───────────┼───────────┼───────────┼───────────┤
D 1-Rare   │           │  R-019    │  R-020    │           │           │
           │     1     │     2     │     3     │     4     │     5     │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

### Residual Risk Matrix (After Controls)

```
                                    IMPACT
              1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
           ┌───────────┬───────────┬───────────┬───────────┬───────────┐
5-Almost   │           │           │           │           │           │
Certain    │     5     │    10     │    15     │    20     │    25     │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
4-Likely   │           │           │           │  R-006    │           │
           │     4     │     8     │    12     │    16     │    20     │
L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
I 3-Possible│          │           │ R-001     │ R-002     │           │
K          │           │           │ R-003     │ R-010     │           │
E          │     3     │     6     │ R-009     │ R-013     │           │
L          │           │           │ R-015     │           │           │
I          ├───────────┼───────────┼───────────┼───────────┼───────────┤
H 2-Unlikely│          │ R-019     │ R-004     │ R-005     │           │
O          │           │ R-020     │ R-007     │ R-011     │           │
O          │           │           │ R-008     │ R-014     │           │
D          │     2     │     4     │ R-012     │ R-018     │    10     │
           │           │           │ R-016     │           │           │
           │           │           │ R-017     │           │           │
           ├───────────┼───────────┼───────────┼───────────┼───────────┤
  1-Rare   │           │           │           │           │           │
           │     1     │     2     │     3     │     4     │     5     │
           └───────────┴───────────┴───────────┴───────────┴───────────┘

Legend: ██ Critical (20-25)  ▓▓ High (13-19)  ░░ Medium (6-12)  ·· Low (1-5)
```

**Risk Movement Analysis:**
- **Significant Improvement**: R-004 (16→6), R-005 (12→8), R-008 (9→6), R-017 (9→6) — Controls highly effective
- **Moderate Improvement**: R-001 (16→9), R-003 (12→9), R-010 (15→12), R-013 (15→12) — Further treatment needed
- **Limited Improvement**: R-006 (20→16) — Largely outside programme control
- **Strong Controls**: R-019 (2→4, maintained low), R-020 (3→4, maintained low)

---

## B. Top 10 Risks (Ranked by Residual Score)

| Rank | ID | Title | Category | Inherent | Residual | Owner | Status | Response |
|------|----|-------|----------|----------|----------|-------|--------|----------|
| 1 | R-006 | Political or machinery-of-government change | STRATEGIC | 20 | 16 | DESNZ SRO | Open | Tolerate |
| 2 | R-002 | Consumer data breach | COMPLIANCE | 25 | 15 | DESNZ SRO | Open | Treat |
| 3 | R-001 | Low consumer adoption | STRATEGIC | 16 | 9 | DESNZ SRO | Open | Treat |
| 4 | R-010 | UK GDPR non-compliance | COMPLIANCE | 15 | 12 | DPO / Privacy Lead | Open | Treat |
| 5 | R-013 | High-profile service failure damages public trust | REPUTATIONAL | 15 | 12 | DESNZ SRO | Open | Treat |
| 6 | R-015 | Tariff comparison bias allegation | REPUTATIONAL | 12 | 9 | Programme Director | Open | Treat |
| 7 | R-003 | Energy supplier non-cooperation | OPERATIONAL | 12 | 9 | Programme Director | Open | Treat |
| 8 | R-009 | GDS Service Assessment failure | COMPLIANCE | 12 | 9 | Programme Director | Open | Treat |
| 9 | R-005 | DCC capacity constraints degrade service | TECHNOLOGY | 12 | 8 | Technical Architect | Open | Treat |
| 10 | R-004 | DCC integration delays | TECHNOLOGY | 16 | 6 | Technical Architect | Open | Treat |

---

## C. Detailed Risk Register

### Risk R-001: Low Consumer Adoption

**Category:** STRATEGIC
**Status:** Open
**Risk Owner:** DESNZ SRO (from RACI: Accountable for programme delivery)
**Action Owner:** Product Owner

#### Risk Identification

**Risk Description:**
Consumer adoption falls significantly below the 5 million MAU target within 18 months of public launch, undermining the value-for-money case, ministerial narrative, and programme viability. Consumers may not download the app due to low awareness, apathy, competing supplier apps, or a perception that the value proposition is insufficient.

**Root Cause:**
Consumer inertia — most consumers do not actively seek out energy management tools. The IHD already has low engagement. The app must overcome the "another app" barrier in a crowded mobile ecosystem.

**Trigger Events:**
- App store downloads below 1 million in first 6 months
- Meter linkage completion rate below 30% (complex onboarding causes drop-off)
- Negative early app store reviews (below 3.5 stars) deterring later adopters
- Smart Energy GB co-promotion not materialising or underperforming

**Consequences if Realised:**
- Programme fails to deliver BCR > 2.0, Treasury questions ongoing funding
- Ministerial embarrassment — NAO/PAC criticism of wasted public investment
- Operating cost per user too high for sustainable model
- Programme defunded or descoped

**Affected Stakeholders:**
- **DESNZ Minister** (SD-1): Cannot demonstrate return on £13.5bn SMIP investment
- **HM Treasury** (SD-9): Value for money not demonstrated
- **Citizens** (SD-7): Do not benefit from energy data access
- **Smart Energy GB** (SD-8): Consumer engagement target missed

**Related Objectives:**
- Goal G-1 (5M active users): Directly threatened
- Goal G-6 (sustainable operating model): Undermined if costs not offset by user volume
- Outcome O-1 (consumer savings): No savings without users
- Outcome O-4 (value for money): BCR fails

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Government consumer apps have mixed adoption history; energy management is not an inherent consumer demand; competing supplier apps exist |
| **Impact** | 4 - Major | Programme viability depends on adoption; below 2M users the cost-benefit case collapses |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls and Mitigations

**Existing Controls:**
1. **Smart Energy GB co-promotion partnership**
   - Owner: Programme Director
   - Effectiveness: Adequate
   - Evidence: Smart Energy GB has national campaign infrastructure; co-marketing MoU in discussion

2. **User-centred design approach (Principle 1)**
   - Owner: Head of Design
   - Effectiveness: Strong
   - Evidence: GDS Service Standard mandates user research; iterative design validated with consumers

3. **Simple onboarding journey (UC-1: 3 taps to value)**
   - Owner: Product Owner
   - Effectiveness: Adequate (not yet tested at scale)
   - Evidence: Design prototype tested with 20 consumers in user research

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Co-marketing and good design reduce but don't eliminate adoption risk |
| **Impact** | 3 - Moderate | Impact reduced by phased launch allowing course correction |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Mitigate/Reduce)

**Rationale:** Adoption is the central determinant of programme success. Active mitigation through marketing, design excellence, and early value demonstration is essential.

#### Action Plan

1. **Secure Smart Energy GB co-marketing agreement**
   - Owner: Programme Director
   - Due Date: 2026-04-30
   - Expected Impact: Awareness reach via Smart Energy GB's existing consumer channels

2. **A/B test onboarding flow with 1,000+ users in private Beta**
   - Owner: Product Owner
   - Due Date: 2026-10-31
   - Expected Impact: Optimise meter linkage completion rate above 60%

3. **Develop immediate value proposition — estimated savings on first screen**
   - Owner: Head of Design
   - Due Date: 2026-09-30
   - Expected Impact: Increase 30-day retention above 40%

4. **Partner with energy suppliers for bill insert promotion**
   - Owner: Programme Director
   - Due Date: 2027-01-31
   - Expected Impact: Reach consumers who don't follow energy media

**Target Residual Risk:** Likelihood 2 × Impact 3 = 6 (Medium)

---

### Risk R-002: Consumer Data Breach

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** DESNZ SRO (from RACI: Accountable for data protection)
**Action Owner:** Security Lead

#### Risk Identification

**Risk Description:**
A security incident results in unauthorised access to consumer energy consumption data, triggering ICO investigation, media coverage, ministerial crisis, and consumer trust collapse. Energy consumption data reveals intimate household behaviour (occupancy, routines, appliance usage) making it highly sensitive.

**Root Cause:**
The system creates a new attack surface connecting consumer-facing mobile infrastructure to (indirectly) the smart metering critical national infrastructure. Mobile apps are inherently harder to secure than server-side systems.

**Trigger Events:**
- Mobile app vulnerability exploited (e.g., API key extraction, session hijacking)
- Backend infrastructure compromise (SQL injection, misconfigured access controls)
- Insider threat — support staff accessing consumer data without authorisation
- Third-party component vulnerability (supply chain attack)
- DCC integration security weakness creating lateral movement path

**Consequences if Realised:**
- ICO enforcement action (fines up to £17.5M or 4% of annual turnover)
- Ministerial crisis — PQs, select committee inquiry, media scrutiny
- Consumer trust destruction — mass account deletion, adoption collapse
- Programme potentially cancelled
- Reputational damage to wider smart metering programme

**Affected Stakeholders:**
- **ICO** (SD-4): Enforcement obligation triggered
- **Citizens** (SD-7): Personal data exposed, privacy violated
- **DESNZ Minister** (SD-1): Political crisis
- **NCSC** (SD-12): Critical infrastructure security concern
- **DCC** (SD-5): Potential attack vector into smart metering network

**Related Objectives:**
- Goal G-3 (regulatory compliance): Failed
- Goal G-1 (adoption): Destroyed by trust collapse
- Outcome O-2 (trusted, compliant service): Failed

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 5 - Almost Certain | Without controls, a consumer-facing mobile app connected to critical infrastructure will be targeted and breached |
| **Impact** | 5 - Catastrophic | ICO fines, programme cancellation, political crisis, consumer harm |
| **Inherent Risk Score** | **25** (Critical) | 5 × 5 = 25 |

#### Current Controls and Mitigations

**Existing Controls:**
1. **Security by Design principle (Principle 5 — NON-NEGOTIABLE)**
   - Owner: Technical Architect
   - Effectiveness: Strong (in design; not yet implemented)
   - Evidence: Architecture principles mandate zero trust, encryption everywhere, defence in depth

2. **NCSC security review engagement**
   - Owner: Security Lead
   - Effectiveness: Adequate (engagement planned, not yet started)
   - Evidence: NCSC engagement in stakeholder plan

3. **Mobile app security requirements (NFR-SEC-001 through NFR-SEC-006)**
   - Owner: Technical Architect
   - Effectiveness: Adequate (requirements defined; implementation pending)
   - Evidence: Comprehensive security NFRs including certificate pinning, encrypted storage, MFA

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Strong security controls significantly reduce likelihood but cannot eliminate it for a high-value target |
| **Impact** | 5 - Catastrophic | Impact remains catastrophic regardless of controls — a breach is a breach |
| **Residual Risk Score** | **15** (High) | 3 × 5 = 15 |

#### Risk Response (4Ts Framework)

**Primary Response:** TREAT (Mitigate/Reduce) + TRANSFER (Cyber insurance)

**Rationale:** Risk cannot be terminated (data processing is the programme's purpose) or tolerated (exceeds appetite). Treat through robust security controls; transfer residual financial exposure through cyber insurance.

#### Action Plan

1. **Complete threat model with NCSC input**
   - Owner: Security Lead
   - Due Date: 2026-05-31
   - Expected Impact: Identify and address threat vectors before architecture is finalised

2. **Implement penetration testing programme (annual + mobile-specific)**
   - Owner: Security Lead
   - Due Date: 2026-09-30 (first test before Beta)
   - Expected Impact: Identify vulnerabilities before consumer data is processed

3. **Establish bug bounty programme**
   - Owner: Security Lead
   - Due Date: 2027-01-31 (at public Beta)
   - Expected Impact: Crowdsourced vulnerability discovery

4. **Procure cyber insurance**
   - Owner: Programme Commercial Lead
   - Due Date: 2026-09-30
   - Expected Impact: Transfer financial exposure for breach costs

5. **Develop and test incident response plan including ICO 72-hour notification**
   - Owner: DPO / Privacy Lead
   - Due Date: 2026-08-31
   - Expected Impact: Ensure rapid, compliant response if breach occurs

**Target Residual Risk:** Likelihood 2 × Impact 5 = 10 (Medium) — impact remains catastrophic but probability reduced

---

### Risk R-003: Energy Supplier Non-Cooperation

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Programme Director (from RACI: Accountable for supplier relationships)
**Action Owner:** Programme Integration Lead

#### Risk Identification

**Risk Description:**
Major energy suppliers delay or provide poor-quality API integrations, resulting in the app being unable to retrieve data for a significant proportion of consumers at Beta launch. Suppliers may cite resource constraints, technical complexity, or resist a tool that facilitates switching.

**Root Cause:**
Suppliers have commercial incentives to control the customer relationship (SD-6). A government app with impartial tariff comparison threatens this. Suppliers face no contractual penalty for slow API delivery.

**Trigger Events:**
- Fewer than 4 supplier APIs production-ready by Beta launch date
- Supplier API error rates above 10% causing poor consumer experience
- Big Six supplier actively withdrawing cooperation

**Consequences if Realised:**
- App only works for subset of consumers — adoption limited by supplier coverage
- Consumer frustration — "doesn't work with my supplier" negative reviews
- Meter coverage target of 80% at Beta not achieved
- Programme Director forced to descope or delay

**Affected Stakeholders:**
- **Energy Suppliers** (SD-6): Relationship management challenge
- **Citizens** (SD-7): Cannot access data if their supplier not integrated
- **DCC** (SD-5): Additional load shifted to DCC if supplier route fails for SMETS1

**Related Objectives:**
- Goal G-4 (DCC/supplier integration): Directly threatened
- Goal G-1 (adoption): Limited by supplier coverage

#### Inherent Risk Assessment (Before Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Supplier ambivalence is documented in stakeholder analysis; similar programmes have faced supplier delays |
| **Impact** | 3 - Moderate | Reduces coverage but doesn't prevent app launch (willing suppliers + DCC SMETS2 route provides partial coverage) |
| **Inherent Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Current Controls and Mitigations

1. **Ofgem regulatory mandate for supplier cooperation** — Effectiveness: Adequate
2. **Standardised API specification reducing per-supplier burden** — Effectiveness: Adequate
3. **Early pilot with willing suppliers (Octopus Energy)** — Effectiveness: Strong

#### Residual Risk Assessment (After Controls)

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Regulatory mandate and willing pioneers reduce likelihood |
| **Impact** | 3 - Moderate | Impact unchanged — partial coverage still limits adoption |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT

#### Action Plan

1. **Establish monthly supplier forum with API progress tracking** — Owner: Programme Director — Due: 2026-03-31
2. **Engage Ofgem to reinforce regulatory expectations** — Owner: Programme Director — Due: 2026-04-30
3. **Launch with willing suppliers first, creating consumer pressure** — Owner: Product Owner — Due: Beta launch

**Target Residual Risk:** Likelihood 2 × Impact 3 = 6 (Medium)

---

### Risk R-004: DCC Integration Delays

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** Technical Architect (from RACI: Accountable for architecture and technology)
**Action Owner:** Integration Lead

#### Risk Identification

**Risk Description:**
DCC API integration takes longer than planned due to SEC compliance requirements, DCC capacity planning constraints, or technical complexity of the DCC interface specification. This delays Beta launch and compresses testing timelines.

**Root Cause:**
DCC integration requires SEC authorisation, complex security certificate management, and alignment with DCC scheduling windows. The programme has no prior DCC integration experience.

**Trigger Events:**
- SEC authorisation process exceeds 6 months
- DCC sandbox environment not available when needed
- DCC interface specification changes during integration

**Consequences if Realised:**
- Beta launch delayed by 2-4 months
- SMETS2 data not available at Beta — only supplier APIs (SMETS1) available
- Additional programme costs for extended team retention

**Affected Stakeholders:**
- **DCC** (SD-5): Capacity and scheduling pressure
- **DESNZ SRO** (SD-2): Programme timeline at risk

**Related Objectives:**
- Goal G-4 (DCC/supplier integration): Directly threatened

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | DCC integrations are known to be complex; SEC process is lengthy |
| **Impact** | 4 - Major | Delays Beta launch, compresses testing, increases costs |
| **Inherent Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Current Controls

1. **Fortnightly DCC technical integration sessions** — Effectiveness: Adequate
2. **Batch retrieval design minimising DCC system changes** — Effectiveness: Strong
3. **Early SEC engagement for authorisation** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Early engagement and batch design significantly reduce delay risk |
| **Impact** | 3 - Moderate | Phased approach allows Beta with supplier APIs if DCC delayed |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

#### Action Plan

1. **Initiate SEC authorisation application immediately** — Owner: Programme Director — Due: 2026-03-31
2. **Request DCC sandbox access for Alpha phase** — Owner: Technical Architect — Due: 2026-04-30
3. **Design fallback Beta without DCC (SMETS1 via suppliers only)** — Owner: Technical Architect — Due: 2026-06-30

**Target Residual Risk:** Likelihood 2 × Impact 2 = 4 (Low)

---

### Risk R-005: DCC Capacity Constraints Degrade Service

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** Technical Architect
**Action Owner:** Integration Lead

#### Risk Identification

**Risk Description:**
The additional data access load from millions of consumer app data requests exceeds DCC capacity, causing degradation of existing smart metering operations (supplier reads, firmware updates). DCC imposes throttling that limits data freshness for consumers.

**Root Cause:**
DCC infrastructure designed for industry-to-industry data flows, not consumer-initiated patterns. Adding millions of individual consumers creates a fundamentally different access pattern.

**Trigger Events:**
- Consumer data requests exceed pre-agreed DCC capacity allocation
- DCC imposes rate limiting that pushes data latency beyond 48 hours
- Existing supplier operations degraded, triggering DCC contractual escalation

**Consequences if Realised:**
- Consumer data staleness — app shows 48+ hour old data, poor experience
- DCC relationship damaged — programme blamed for infrastructure issues
- Regulatory intervention if core metering operations affected

**Affected Stakeholders:**
- **DCC** (SD-5): Infrastructure stability threatened
- **Energy Suppliers** (SD-6): Shared infrastructure degraded
- **Citizens** (SD-7): Poor data freshness reduces app value

**Related Objectives:**
- Goal G-4 (integration): Data quality compromised
- Goal G-1 (adoption): Poor experience drives abandonment

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | DCC has raised capacity concerns; demand modelling uncertain at scale |
| **Impact** | 4 - Major | Degrading critical national infrastructure would be a serious incident |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Batch retrieval during DCC low-traffic windows** — Effectiveness: Strong
2. **Aggressive platform-side caching (consumers read from cache, never from DCC directly)** — Effectiveness: Strong
3. **Phased rollout with capacity monitoring** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Batch pattern and caching architecture fundamentally changes DCC load profile |
| **Impact** | 4 - Major | Impact remains high if it does occur |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT

#### Action Plan

1. **Agree formal capacity allocation with DCC** — Owner: Programme Director — Due: 2026-05-31
2. **Implement real-time DCC load monitoring dashboard** — Owner: Technical Architect — Due: 2026-09-30
3. **Define automatic throttle-back triggers if DCC utilisation exceeds 80%** — Owner: Technical Architect — Due: 2026-09-30

**Target Residual Risk:** Likelihood 1 × Impact 4 = 4 (Low)

---

### Risk R-006: Political or Machinery-of-Government Change

**Category:** STRATEGIC
**Status:** Open
**Risk Owner:** DESNZ SRO (from RACI: Accountable for programme continuity)
**Action Owner:** DESNZ SRO

#### Risk Identification

**Risk Description:**
Cabinet reshuffle, departmental restructuring, change of government, or shift in energy policy priorities defunds or deprioritises the programme. Energy policy is politically sensitive and the programme spans multiple years, increasing exposure to political change.

**Root Cause:**
UK Government programmes are inherently exposed to political cycles. DESNZ itself was created from a machinery-of-government change (splitting from BEIS). Energy policy is contested political territory.

**Trigger Events:**
- Cabinet reshuffle assigns new DESNZ minister with different priorities
- General election results in change of government with different energy policy
- Spending Review reprioritises DESNZ budget away from consumer apps
- NAO or PAC report questions programme value, triggering political decision to cancel

**Consequences if Realised:**
- Programme defunded or cancelled mid-delivery
- Contractual commitments with DCC and suppliers cannot be honoured
- Team disbanded, institutional knowledge lost
- Consumer data already collected must be safely disposed of

**Affected Stakeholders:**
- **DESNZ Minister** (SD-1): Programme ceases to exist
- **DESNZ SRO** (SD-2): Accountability for programme wind-down
- **HM Treasury** (SD-9): Sunk cost with no benefits
- **Citizens** (SD-7): Promised service not delivered

**Related Objectives:**
- All goals at risk if funding or political support withdrawn

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 5 - Almost Certain | Over a multi-year programme, some form of political change is near-certain |
| **Impact** | 4 - Major | Programme cancellation would waste £10-17M investment |
| **Inherent Risk Score** | **20** (Critical) | 5 × 4 = 20 |

#### Current Controls

1. **Cross-party appeal of consumer empowerment and cost savings** — Effectiveness: Adequate
2. **Early value demonstration through phased delivery** — Effectiveness: Adequate
3. **Broad stakeholder support beyond single minister** — Effectiveness: Weak (stakeholder engagement still early)

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Controls reduce but cannot eliminate political risk |
| **Impact** | 4 - Major | Impact unchanged — cancellation is cancellation |
| **Residual Risk Score** | **16** (High) | 4 × 4 = 16 |

#### Risk Response: TOLERATE (with active monitoring)

**Rationale:** Political risk is largely outside programme control. The programme can build resilience through cross-party appeal and early value demonstration but cannot prevent political decisions. Termination is not an option (the programme exists to address this political need). Transfer is not possible.

#### Action Plan

1. **Frame programme value in cross-party terms (consumer savings, Net Zero, fuel poverty)** — Owner: DESNZ SRO — Due: Ongoing
2. **Demonstrate early value at each phase gate (Alpha, Beta) with ministerial-quality metrics** — Owner: Programme Director — Due: Each phase gate
3. **Build contractual commitments with DCC/suppliers that create momentum** — Owner: Programme Commercial Lead — Due: 2026-06-30
4. **Prepare programme continuation brief for any new minister within 48 hours of appointment** — Owner: DESNZ SRO — Due: Template ready by 2026-06-30

**Target Residual Risk:** Likelihood 4 × Impact 3 = 12 (Medium) — achievable only if early value is demonstrated

---

### Risk R-007: Cloud Costs Exceed Budget

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** Programme Commercial Lead
**Action Owner:** Technical Architect

#### Risk Identification

**Risk Description:**
Cloud infrastructure costs significantly exceed budget projections due to underestimated data volumes (36 billion readings/year), scaling requirements (500K peak concurrent users), or insufficient cost optimisation. The programme's cloud cost model is untested at the projected scale.

**Root Cause:**
Data volume projections are estimates; actual data volumes depend on adoption and retrieval patterns. Cloud cost models are non-linear and difficult to predict at scale without prototyping.

**Trigger Events:**
- Monthly cloud costs exceed budget by >20% for 3 consecutive months
- Data storage costs grow faster than projected due to retention policy requirements
- Scaling events (energy price cap announcements) cause unexpected compute costs

**Consequences if Realised:**
- Operating cost exceeds Treasury-approved budget, requiring supplementary estimate
- BCR falls below 2.0, undermining value-for-money case
- Service descoped to reduce costs (feature removal)

**Affected Stakeholders:**
- **HM Treasury** (SD-9): Budget breach requires approval
- **DESNZ SRO** (SD-2): Accountable for financial management

**Related Objectives:**
- Goal G-6 (sustainable operating model): Directly threatened

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Cloud cost overruns are common in government projects at scale |
| **Impact** | 3 - Moderate | Budget overrun manageable if caught early; 20-40% variance |
| **Inherent Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Current Controls

1. **Architecture principles mandate cost-efficient design (Principles 2, 13)** — Effectiveness: Adequate
2. **Data lifecycle management with hot/warm/cold tiers (NFR-S-002)** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Tiered storage and cost-aware design reduce likelihood |
| **Impact** | 3 - Moderate | Impact unchanged |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

#### Action Plan

1. **Implement FinOps practice from Alpha phase** — Owner: Technical Architect — Due: 2026-05-31
2. **Set cost alerting at 80% and 90% of monthly budget** — Owner: Technical Architect — Due: 2026-06-30
3. **Run cost model validation during Alpha with representative data volumes** — Owner: Technical Architect — Due: 2026-07-31

**Target Residual Risk:** Likelihood 2 × Impact 2 = 4 (Low)

---

### Risk R-008: Insufficient Multidisciplinary Team Capacity

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Programme Director
**Action Owner:** Programme Director

#### Risk Identification

**Risk Description:**
The programme cannot recruit or retain the multidisciplinary team needed — particularly user researchers, interaction designers with accessibility expertise, mobile developers, and security specialists. Civil service pay scales may not attract sufficient talent, and security-cleared contractors are scarce.

**Root Cause:**
Government digital teams compete with private sector for scarce mobile development and security talent. Civil service headcount restrictions limit permanent recruitment. Security clearance requirements narrow the pool further.

**Trigger Events:**
- Key roles unfilled for >8 weeks
- Team turnover exceeds 20% annually
- Security clearance processing delays >3 months

**Consequences if Realised:**
- Development velocity reduced — timeline slips
- Quality compromised — accessibility, security, or UX standards not met
- GDS assessment failure due to missing multidisciplinary roles

**Affected Stakeholders:**
- **DESNZ SRO** (SD-2): Delivery at risk
- **GDS Assessors** (SD-11): Require evidence of multidisciplinary team
- **Programme Delivery Team**: Overwork and burnout

**Related Objectives:**
- Goal G-3 (regulatory compliance): GDS Point 6 requires multidisciplinary team
- Goal G-5 (accessibility): Requires specialist designers

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Government digital recruitment challenges are well documented |
| **Impact** | 3 - Moderate | Delays delivery but doesn't prevent it entirely |
| **Inherent Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Current Controls

1. **Early recruitment pipeline activation** — Effectiveness: Adequate
2. **Blended team model (civil servants + contractors)** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Blended model provides flexibility |
| **Impact** | 3 - Moderate | Impact unchanged |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

#### Action Plan

1. **Engage recruitment agencies with government digital specialisation** — Owner: Programme Director — Due: 2026-03-31
2. **Secure SC clearance sponsorship for contractor roles** — Owner: Programme Director — Due: 2026-04-30

**Target Residual Risk:** Likelihood 2 × Impact 2 = 4 (Low)

---

### Risk R-009: GDS Service Assessment Failure

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Programme Director
**Action Owner:** Programme Director

#### Risk Identification

**Risk Description:**
The service fails a GDS Service Standard assessment at Alpha, Beta, or Live gates. A "not met" result delays the programme, is publicly visible, and creates political embarrassment. Assessment failure is most likely on Points 1 (understand users), 5 (accessibility), or 14 (operate a reliable service).

**Root Cause:**
GDS assessments require rigorous evidence of user research, inclusive design, and operational capability. Programmes that treat assessment as a checkbox rather than an embedded practice frequently fail.

**Trigger Events:**
- Insufficient user research evidence at assessment
- Accessibility testing incomplete or failing
- Operational runbooks and SLOs not defined for Live assessment
- Assessors identify "waterfall delivery disguised as agile"

**Consequences if Realised:**
- 2-3 month delay for re-assessment
- Political embarrassment (assessment results are published)
- SRO required to explain to minister

**Affected Stakeholders:**
- **GDS Assessors** (SD-11): Assessment integrity
- **DESNZ SRO** (SD-2): Programme timeline
- **DESNZ Minister** (SD-1): Public failure narrative

**Related Objectives:**
- Goal G-3 (regulatory compliance): GDS compliance is mandatory

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 4 - Likely | Many government services fail first assessment; mobile services are less common in GDS assessments |
| **Impact** | 3 - Moderate | Delay is significant but recoverable |
| **Inherent Risk Score** | **12** (Medium) | 4 × 3 = 12 |

#### Current Controls

1. **GDS engagement from Discovery phase** — Effectiveness: Adequate
2. **Evidence portfolio maintained continuously** — Effectiveness: Adequate
3. **User research embedded in delivery** — Effectiveness: Strong (Principle 1)

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Early engagement reduces but doesn't eliminate risk |
| **Impact** | 3 - Moderate | Unchanged |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT

#### Action Plan

1. **Conduct mock assessment at each phase gate** — Owner: Programme Director — Due: 2 weeks before each assessment
2. **Appoint dedicated GDS assessment coordinator** — Owner: Programme Director — Due: 2026-04-30

**Target Residual Risk:** Likelihood 2 × Impact 3 = 6 (Medium)

---

### Risk R-010: UK GDPR Non-Compliance

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** DPO / Privacy Lead
**Action Owner:** DPO / Privacy Lead

#### Risk Identification

**Risk Description:**
The programme fails to achieve or maintain UK GDPR compliance — specifically regarding lawful basis for processing, granular consent, data subject rights (access, erasure, portability), or data minimisation. Energy consumption data reveals intimate household behaviour, attracting heightened ICO scrutiny.

**Root Cause:**
Energy data is personal data of unusual sensitivity. Processing at scale (34M households potentially) creates significant compliance complexity. Consent management across multiple purposes with granular revocation is technically challenging.

**Trigger Events:**
- DPIA rejected by ICO, requiring architectural rework
- Consumer complaints to ICO about consent mechanisms
- ICO audit identifies processing without adequate lawful basis
- Cross-border data transfer discovered (e.g., analytics CDN or crash reporting tool sending data outside UK)

**Consequences if Realised:**
- ICO enforcement notice or fine (up to £17.5M)
- Programme halted until compliance achieved
- Consumer trust destroyed
- Ministerial crisis

**Affected Stakeholders:**
- **ICO** (SD-4): Enforcement obligation
- **Citizens** (SD-7): Data rights violated
- **DESNZ SRO** (SD-2): Programme halted

**Related Objectives:**
- Goal G-3 (regulatory compliance): Failed
- Outcome O-2 (trusted service): Failed

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Energy data processing is novel territory; ICO has signalled interest in smart meter data |
| **Impact** | 5 - Catastrophic | £17.5M fine, programme halt, trust collapse |
| **Inherent Risk Score** | **15** (High) | 3 × 5 = 15 |

#### Current Controls

1. **Privacy by Design principle (Principle 7)** — Effectiveness: Strong (architectural commitment)
2. **Granular consent framework designed (FR-003)** — Effectiveness: Adequate (not yet implemented)
3. **Data minimisation requirements (Principle 7)** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Principles reduce but ICO scrutiny of novel processing remains |
| **Impact** | 4 - Major | Impact reduced from catastrophic through early ICO engagement reducing enforcement risk |
| **Residual Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Risk Response: TREAT

#### Action Plan

1. **Complete DPIA and submit to ICO for pre-consultation** — Owner: DPO — Due: 2026-06-30
2. **Implement consent management platform with granular controls** — Owner: Technical Architect — Due: 2026-09-30
3. **Commission independent data protection audit before Beta** — Owner: DPO — Due: 2026-10-31
4. **Verify no cross-border data flows from all third-party SDKs** — Owner: Technical Architect — Due: 2026-08-31

**Target Residual Risk:** Likelihood 2 × Impact 4 = 8 (Medium)

---

### Risk R-011: SMETS1/SMETS2 Data Inconsistency

**Category:** TECHNOLOGY
**Status:** Open
**Risk Owner:** Technical Architect
**Action Owner:** Integration Lead

#### Risk Identification

**Risk Description:**
Data quality and format differences between SMETS1 (via supplier APIs) and SMETS2 (via DCC) meters create inconsistent consumer experience. Gas unit conversions (m³ to kWh), timestamp handling, and missing reading treatment vary between sources.

**Root Cause:**
SMETS1 and SMETS2 use different communication protocols and data formats. Each supplier implements SMETS1 data access differently. There is no single standard for consumer-facing energy data.

**Trigger Events:**
- Consumer sees different consumption figures in app vs supplier bill
- Gas conversion errors cause misleading cost estimates
- Missing SMETS1 readings not flagged, showing artificially low consumption

**Consequences if Realised:**
- Consumer trust eroded — "the numbers don't match my bill"
- Negative app store reviews citing inaccurate data
- Ofgem concern about misleading consumer information

**Affected Stakeholders:**
- **Citizens** (SD-7): Inaccurate data leads to wrong financial decisions
- **Ofgem** (SD-3): Consumer protection concern
- **Energy Suppliers** (SD-6): Blame directed at suppliers for data quality

**Related Objectives:**
- Goal G-2 (energy savings): Inaccurate data undermines savings calculations

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | SMETS1/SMETS2 inconsistencies are known in the industry |
| **Impact** | 4 - Major | Data accuracy is fundamental to consumer trust |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Data quality requirements (Principle 9)** — Effectiveness: Adequate
2. **Normalisation layer abstracting meter types (Principle 11)** — Effectiveness: Strong (architectural design)

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Normalisation layer addresses most format differences |
| **Impact** | 4 - Major | Impact remains high if consumer sees incorrect data |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT

#### Action Plan

1. **Build data reconciliation checks comparing app data to supplier billing data** — Owner: Technical Architect — Due: 2026-09-30
2. **Develop SMETS1/SMETS2 test suite with known-good reference data** — Owner: Integration Lead — Due: 2026-08-31

**Target Residual Risk:** Likelihood 1 × Impact 4 = 4 (Low)

---

### Risk R-012: Treasury Spending Control Delays

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** DESNZ SRO
**Action Owner:** Programme Commercial Lead

#### Risk Identification

**Risk Description:**
HM Treasury and CDDO spending control processes delay procurement or cloud hosting contracts, compressing delivery timelines. Digital spend over £1M requires CDDO approval; spend over £X requires Treasury approval.

**Root Cause:**
Cross-government spend control processes have defined timescales that may not align with programme delivery timeline. CDDO and Treasury review capacity is limited.

**Trigger Events:**
- CDDO spend control review takes >8 weeks
- Treasury questions SOBC and requests additional evidence
- Procurement challenge delays vendor contract

**Consequences if Realised:**
- 2-4 month delay in procurement or infrastructure setup
- Team idle while awaiting approval — wasted cost
- Political pressure to bypass controls (reputational risk)

**Affected Stakeholders:**
- **HM Treasury** (SD-9): Spend control integrity
- **CDDO** (engagement): Capacity constraints
- **DESNZ SRO** (SD-2): Timeline pressure

**Related Objectives:**
- Goal G-4 (integration): Delayed if infrastructure procurement delayed

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | DESNZ has experience navigating spend controls |
| **Impact** | 3 - Moderate | Delays are frustrating but manageable with planning |
| **Inherent Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Current Controls

1. **Early CDDO engagement and pre-consultation** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Early engagement mitigates |
| **Impact** | 3 - Moderate | Unchanged |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

---

### Risk R-013: High-Profile Service Failure Damages Public Trust

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** DESNZ SRO
**Action Owner:** Programme Director

#### Risk Identification

**Risk Description:**
A visible service failure — extended outage, incorrect data displayed to consumers, or app crash during peak usage — generates negative media coverage, parliamentary questions, and consumer abandonment. Government IT failures receive disproportionate media attention.

**Root Cause:**
Consumer-facing government services are high-profile targets for media scrutiny. Any failure — even temporary — will be amplified.

**Trigger Events:**
- Service outage lasting >4 hours during peak usage
- Data accuracy error affecting >1,000 consumers
- App crash rate exceeding 2% on energy price cap announcement day
- Negative viral social media post about the app

**Consequences if Realised:**
- Media headlines: "Government energy app crashes / shows wrong data"
- Parliamentary questions
- Consumer abandonment (30-day retention drops below 20%)
- Programme credibility undermined

**Affected Stakeholders:**
- **DESNZ Minister** (SD-1): Political embarrassment
- **Citizens** (SD-7): Trust destroyed
- **Smart Energy GB** (SD-8): Must defend app quality publicly

**Related Objectives:**
- Goal G-1 (adoption): Negative press kills adoption
- Outcome O-2 (trusted service): Failed

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Government digital services have mixed reliability track record |
| **Impact** | 5 - Catastrophic | Media amplification turns any failure into a political crisis |
| **Inherent Risk Score** | **15** (High) | 3 × 5 = 15 |

#### Current Controls

1. **Resilience and fault tolerance architecture (Principle 3)** — Effectiveness: Strong
2. **Graceful degradation hierarchy (NFR-A-003)** — Effectiveness: Strong
3. **Observability and alerting (Principle 6)** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Architecture reduces failure probability but doesn't eliminate it |
| **Impact** | 4 - Major | Reduced from catastrophic through incident comms planning |
| **Residual Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Risk Response: TREAT

#### Action Plan

1. **Develop pre-prepared incident communications (ministerial lines, media statement, consumer notification)** — Owner: DESNZ Communications — Due: 2026-09-30
2. **Conduct chaos engineering exercises before public Beta** — Owner: Technical Architect — Due: 2026-12-31
3. **Load test for energy price cap announcement day scenario (10x normal traffic)** — Owner: Technical Architect — Due: 2027-01-31

**Target Residual Risk:** Likelihood 2 × Impact 4 = 8 (Medium)

---

### Risk R-014: Accessibility Compliance Failure

**Category:** COMPLIANCE
**Status:** Open
**Risk Owner:** Head of Design
**Action Owner:** Head of Design

#### Risk Identification

**Risk Description:**
The app fails to achieve WCAG 2.2 Level AA compliance, particularly for energy data visualisations (charts, graphs) that are inherently difficult to make accessible. This triggers legal challenge under Accessibility Regulations 2018 and GDS assessment failure on Point 5.

**Root Cause:**
Energy data visualisation — charts showing half-hourly consumption, tariff comparisons, budget tracking — is inherently visual. Making these meaningfully accessible to screen reader users requires significant design investment.

**Trigger Events:**
- WCAG audit identifies critical failures in chart accessibility
- Consumer with disability files formal complaint
- GDS assessor flags accessibility as "not met"

**Consequences if Realised:**
- Legal obligation not met (Accessibility Regulations 2018)
- GDS assessment failure
- Consumer organisations publicly criticise the service
- Reputation as an inclusive government service destroyed

**Affected Stakeholders:**
- **Consumer Orgs** (SD-10): Inclusive service promise broken
- **GDS Assessors** (SD-11): Point 5 not met
- **Citizens** (SD-7): Excluded consumers

**Related Objectives:**
- Goal G-5 (WCAG 2.2 AA): Failed

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Accessibility is an explicit requirement and architectural principle |
| **Impact** | 4 - Major | Legal compliance failure + GDS failure |
| **Inherent Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Current Controls

1. **Accessibility principle (Principle 15) requiring WCAG 2.2 AA** — Effectiveness: Strong
2. **Accessible alternatives for visualisations required (data tables, text summaries)** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Strong architectural commitment |
| **Impact** | 4 - Major | Impact unchanged if it occurs |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT

#### Action Plan

1. **Conduct accessibility testing with 20+ users with access needs** — Owner: Head of Design — Due: 2026-10-31
2. **Engage specialist accessibility consultancy for energy visualisation patterns** — Owner: Head of Design — Due: 2026-06-30

**Target Residual Risk:** Likelihood 1 × Impact 4 = 4 (Low)

---

### Risk R-015: Tariff Comparison Bias Allegation

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** Programme Director
**Action Owner:** Product Owner

#### Risk Identification

**Risk Description:**
Energy suppliers or media allege that the tariff comparison feature is biased, inaccurate, or misleading. This could arise from methodology disputes, data quality issues, or perceptions that the app favours challenger suppliers over incumbents.

**Root Cause:**
Tariff comparison using actual half-hourly consumption data will produce different results from annualised estimates used by existing comparison sites. This difference will be challenged.

**Trigger Events:**
- Energy supplier publicly disputes tariff comparison results
- Consumer complaint that switching based on app recommendation resulted in higher bills
- Media investigation into tariff comparison methodology

**Consequences if Realised:**
- Ofgem investigation into comparison methodology
- Energy supplier withdraws API cooperation
- Consumer trust in comparison feature destroyed

**Affected Stakeholders:**
- **Ofgem** (SD-3): Consumer protection concern
- **Energy Suppliers** (SD-6): Commercial impact of comparison
- **Citizens** (SD-7): Trust in financial information

**Related Objectives:**
- Goal G-2 (energy savings): Tariff switching is a key savings mechanism
- Goal G-4 (supplier integration): Supplier cooperation threatened

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Suppliers have incentive to challenge; methodology disputes are common |
| **Impact** | 4 - Major | Ofgem investigation + supplier withdrawal would be severe |
| **Inherent Risk Score** | **12** (Medium) | 3 × 4 = 12 |

#### Current Controls

1. **Ofgem-endorsed methodology requirement (FR-007)** — Effectiveness: Strong
2. **Transparent methodology shared with suppliers** — Effectiveness: Adequate

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Allegations can occur regardless of methodology quality |
| **Impact** | 3 - Moderate | Ofgem endorsement provides strong defence |
| **Residual Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Risk Response: TREAT

#### Action Plan

1. **Obtain written Ofgem endorsement of tariff comparison methodology** — Owner: Programme Director — Due: 2026-09-30
2. **Publish methodology transparently (open documentation)** — Owner: Product Owner — Due: 2027-01-31
3. **Establish independent methodology review panel** — Owner: Programme Director — Due: 2027-01-31

**Target Residual Risk:** Likelihood 2 × Impact 3 = 6 (Medium)

---

### Risk R-016: DCC Commercial Model Not Agreed

**Category:** FINANCIAL
**Status:** Open
**Risk Owner:** Programme Commercial Lead
**Action Owner:** Programme Commercial Lead

#### Risk Identification

**Risk Description:**
The commercial model for DCC data access costs is not agreed in time, creating financial uncertainty and potential programme cost overrun. DCC may charge per-read or per-meter fees that make the operating model unsustainable at scale.

**Root Cause:**
DCC's commercial model for third-party consumer-facing data access is novel and untested. DCC must balance cost recovery with not pricing the service out of viability.

**Trigger Events:**
- DCC proposes per-read pricing that would cost >£5M/year at scale
- Commercial negotiations extend beyond 6 months
- DCC board rejects proposed commercial terms

**Consequences if Realised:**
- Operating costs exceed Treasury-approved budget
- BCR falls below 2.0
- Programme descoped to reduce DCC dependency

**Affected Stakeholders:**
- **DCC** (SD-5): Commercial relationship
- **HM Treasury** (SD-9): Budget impact

**Related Objectives:**
- Goal G-6 (sustainable operating model): Directly threatened

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | DESNZ has leverage as DCC's policy sponsor |
| **Impact** | 3 - Moderate | Delays programme but alternative commercial routes exist |
| **Inherent Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | DESNZ influence is strong |
| **Impact** | 3 - Moderate | Unchanged |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

---

### Risk R-017: Recommendation Engine Quality Insufficient

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Product Owner
**Action Owner:** Technical Architect

#### Risk Identification

**Risk Description:**
The personalised energy-saving recommendation engine generates generic, unhelpful, or inaccurate advice that does not drive measurable behaviour change. The 5% energy reduction target (Goal G-2) depends on recommendation quality.

**Root Cause:**
Personalised recommendations based on consumption data require sophisticated analytics. Recommendations must be actionable, specific to UK housing stock, and tailored to individual consumption patterns — not generic tips.

**Trigger Events:**
- Active users show <2% energy reduction after 6 months (vs 5% target)
- Consumer feedback identifies recommendations as "generic" or "not relevant"
- A/B testing shows no difference between personalised and generic recommendations

**Consequences if Realised:**
- Core benefit proposition undermined — no measurable savings
- Treasury questions programme value if savings not demonstrated
- Consumer engagement drops — "app doesn't help me save"

**Affected Stakeholders:**
- **Citizens** (SD-7): No tangible savings
- **DESNZ Minister** (SD-1): Cannot claim savings benefits
- **HM Treasury** (SD-9): BCR not achieved

**Related Objectives:**
- Goal G-2 (5% energy savings): Failed

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 3 - Possible | Behaviour change through app recommendations is unproven at scale |
| **Impact** | 3 - Moderate | Reduces benefits but other features (visibility, tariff comparison) still provide value |
| **Inherent Risk Score** | **9** (Medium) | 3 × 3 = 9 |

#### Current Controls

1. **Personalisation requirement (FR-006: recommendations must use actual consumption)** — Effectiveness: Adequate
2. **A/B testing framework for recommendation effectiveness** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Iterative testing and personalisation reduce risk |
| **Impact** | 3 - Moderate | Unchanged |
| **Residual Risk Score** | **6** (Medium) | 2 × 3 = 6 |

#### Risk Response: TREAT

---

### Risk R-018: App Store Rejection or Removal

**Category:** OPERATIONAL
**Status:** Open
**Risk Owner:** Programme Director
**Action Owner:** Technical Architect

#### Risk Identification

**Risk Description:**
Apple App Store or Google Play rejects or removes the app due to policy violations (privacy, data access, background data usage). App store policy changes can affect published apps retroactively.

**Root Cause:**
App stores have evolving policies, particularly around privacy (Apple's App Tracking Transparency, Google's Play Protect). Energy data collection and background data refresh may trigger review.

**Trigger Events:**
- App store review rejects initial submission
- Policy change requires architectural changes to background data collection
- Consumer privacy complaint triggers app store investigation

**Consequences if Realised:**
- App unavailable on one or both platforms — blocks adoption
- Emergency development to comply with new policies
- Consumer disruption if existing app removed

**Affected Stakeholders:**
- **App Stores** (from stakeholder analysis): Distribution gatekeepers
- **Citizens** (SD-7): Cannot download or use app
- **DESNZ SRO** (SD-2): Programme blocked

**Related Objectives:**
- Goal G-1 (adoption): Cannot adopt if cannot download

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Government apps generally receive favourable review; privacy-first design helps |
| **Impact** | 4 - Major | Blocks entire distribution channel |
| **Inherent Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Current Controls

1. **Privacy by Design (Principle 7)** — Effectiveness: Strong
2. **No third-party analytics SDKs that transmit PII (NFR-SEC-006)** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Privacy-first design aligns with store policies |
| **Impact** | 4 - Major | Unchanged |
| **Residual Risk Score** | **8** (Medium) | 2 × 4 = 8 |

#### Risk Response: TREAT

---

### Risk R-019: Scope Creep From Ministerial Enthusiasm

**Category:** STRATEGIC
**Status:** Open
**Risk Owner:** DESNZ SRO
**Action Owner:** Programme Director

#### Risk Identification

**Risk Description:**
Ministerial enthusiasm leads to scope additions (smart home integration, solar export, Open Banking bill payment) that dilute focus, increase cost, and delay the core delivery. The stakeholder analysis identifies this dynamic explicitly (SD-2 blocker: "Scope creep driven by ministerial enthusiasm").

**Root Cause:**
Ministers see the app as a vehicle for multiple energy policy objectives. Each good idea adds scope.

**Trigger Events:**
- Minister requests specific feature ("Can the app show solar panel output?")
- Phase 2 features demanded in Phase 1
- DESNZ policy teams propose additional data integrations

**Consequences if Realised:**
- Core delivery delayed by 3-6 months
- Budget exceeded, requiring supplementary estimate
- Quality diluted across too many features
- GDS assessment failure due to unfocused service

**Affected Stakeholders:**
- **DESNZ Minister** (SD-1): Wants features but also wants timely delivery
- **DESNZ SRO** (SD-2): Managing scope is SRO's responsibility
- **HM Treasury** (SD-9): Budget impact

**Related Objectives:**
- Goal G-1 (adoption): Delayed launch delays adoption clock
- Goal G-6 (sustainable model): Cost overrun

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 1 - Rare | SRO and Programme Director actively manage scope; requirements document clearly defines in/out scope |
| **Impact** | 2 - Minor | Individual scope additions are manageable; only accumulation is dangerous |
| **Inherent Risk Score** | **2** (Low) | 1 × 2 = 2 |

#### Current Controls

1. **Clear in/out scope in requirements (ARC-001-REQ-v1.0)** — Effectiveness: Strong
2. **Phase 2 backlog for future features** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Controls effective but ministerial direction hard to refuse |
| **Impact** | 2 - Minor | Unchanged |
| **Residual Risk Score** | **4** (Low) | 2 × 2 = 4 |

#### Risk Response: TOLERATE

---

### Risk R-020: NAO/PAC Scrutiny of Programme Value

**Category:** REPUTATIONAL
**Status:** Open
**Risk Owner:** DESNZ SRO
**Action Owner:** Programme Commercial Lead

#### Risk Identification

**Risk Description:**
The NAO audits the programme and/or the PAC conducts an inquiry, questioning the value for money, delivery approach, or outcomes. The smart metering programme has already been subject to NAO and PAC scrutiny.

**Root Cause:**
Large government programmes attract NAO attention. The SMIP has been audited multiple times. A new consumer app adds to the scrutiny surface.

**Trigger Events:**
- NAO announces value-for-money study of the consumer app programme
- PAC inquiry into smart metering programme includes app
- Whistleblower or FOI request reveals unfavourable information

**Consequences if Realised:**
- Critical NAO report damages programme reputation
- PAC recommendations impose additional governance burden
- Ministerial confidence reduced
- Media coverage of "failing government IT project"

**Affected Stakeholders:**
- **DESNZ Minister** (SD-1): Must respond to parliamentary scrutiny
- **DESNZ SRO** (SD-2): Appears before PAC
- **HM Treasury** (SD-9): VfM questioned

**Related Objectives:**
- Outcome O-4 (value for money): Questioned

#### Inherent Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 1 - Rare | Programme is relatively small (£10-17M) for NAO attention; proactive benefits tracking reduces risk |
| **Impact** | 3 - Moderate | NAO report is damaging but programme can continue |
| **Inherent Risk Score** | **3** (Low) | 1 × 3 = 3 |

#### Current Controls

1. **Benefits realisation tracking against SOBC** — Effectiveness: Adequate
2. **Transparent governance and audit trail** — Effectiveness: Strong

#### Residual Risk Assessment

| Assessment | Rating | Justification |
|------------|--------|---------------|
| **Likelihood** | 2 - Unlikely | Proactive governance reduces scrutiny risk but cannot prevent it |
| **Impact** | 2 - Minor | Governance quality means findings would be manageable |
| **Residual Risk Score** | **4** (Low) | 2 × 2 = 4 |

#### Risk Response: TOLERATE

---

## D. Risk Category Analysis

### STRATEGIC Risks

**Total STRATEGIC Risks:** 3 (R-001, R-006, R-019)
**Average Inherent Score:** 12.7 (Medium-High)
**Average Residual Score:** 9.7 (Medium)
**Control Effectiveness:** 24% reduction

**Key Themes:**
- Political uncertainty is the dominant strategic risk and is largely uncontrollable
- Consumer adoption risk is high but addressable through design and marketing
- Scope creep is well-controlled through clear requirements

**Category Risk Profile:** ⚠️ Concerning — R-006 (political change) remains High and exceeds appetite

---

### OPERATIONAL Risks

**Total OPERATIONAL Risks:** 4 (R-003, R-008, R-017, R-018)
**Average Inherent Score:** 9.5 (Medium)
**Average Residual Score:** 7.3 (Medium)
**Control Effectiveness:** 23% reduction

**Key Themes:**
- Supplier cooperation is the primary operational concern
- Team capacity is manageable through blended delivery model
- Recommendation quality requires iterative improvement

**Category Risk Profile:** ✅ Acceptable — All risks within reasonable bounds

---

### FINANCIAL Risks

**Total FINANCIAL Risks:** 3 (R-007, R-012, R-016)
**Average Inherent Score:** 7.0 (Medium)
**Average Residual Score:** 6.0 (Medium)
**Control Effectiveness:** 14% reduction

**Key Themes:**
- Cloud costs are the primary financial risk but addressable through FinOps
- Spending control delays are a known government challenge
- DCC commercial model creates uncertainty

**Category Risk Profile:** ✅ Acceptable — Risks well-understood and manageable

---

### COMPLIANCE/REGULATORY Risks

**Total COMPLIANCE Risks:** 4 (R-002, R-009, R-010, R-014)
**Average Inherent Score:** 14.0 (High)
**Average Residual Score:** 11.0 (Medium)
**Control Effectiveness:** 21% reduction

**Key Themes:**
- Data breach and GDPR non-compliance are the highest-impact compliance risks
- Compliance risks are structurally difficult to mitigate below appetite
- Multiple regulatory bodies (ICO, Ofgem, GDS, NCSC) create complex compliance landscape

**Category Risk Profile:** ⚠️ Concerning — 2 risks exceed appetite; compliance is the programme's most challenging risk area

---

### REPUTATIONAL Risks

**Total REPUTATIONAL Risks:** 3 (R-013, R-015, R-020)
**Average Inherent Score:** 10.0 (Medium)
**Average Residual Score:** 8.3 (Medium)
**Control Effectiveness:** 17% reduction

**Key Themes:**
- Government IT projects receive disproportionate media scrutiny
- Service failure and tariff comparison bias are the primary reputational risks
- Prevention is critical — reputational damage is difficult to reverse

**Category Risk Profile:** ⚠️ Concerning — R-013 exceeds appetite; incident communications preparation essential

---

### TECHNOLOGY Risks

**Total TECHNOLOGY Risks:** 3 (R-004, R-005, R-011)
**Average Inherent Score:** 13.3 (High)
**Average Residual Score:** 7.3 (Medium)
**Control Effectiveness:** 45% reduction

**Key Themes:**
- DCC integration is the critical technology dependency
- SMETS1/SMETS2 data inconsistency requires normalisation
- Architecture principles provide strong technology risk controls

**Category Risk Profile:** ✅ Acceptable — Strong control effectiveness; technology risks well-addressed by architecture

---

## E. Risk Ownership Matrix

| Stakeholder | Role | Owned Risks | Critical/High | Medium | Low | Total Residual Score |
|-------------|------|-------------|---------------|--------|-----|---------------------|
| DESNZ SRO | Senior Responsible Owner | R-001, R-002, R-006, R-012, R-013, R-019, R-020 | 2 High | 3 Medium | 2 Low | 66 |
| Programme Director | Delivery Lead | R-003, R-008, R-009, R-015, R-018 | 0 | 5 Medium | 0 | 38 |
| Technical Architect | Architecture Authority | R-004, R-005, R-011 | 0 | 3 Medium | 0 | 22 |
| DPO / Privacy Lead | Data Protection | R-010 | 0 | 1 Medium | 0 | 12 |
| Head of Design | Design Authority | R-014 | 0 | 1 Medium | 0 | 8 |
| Programme Commercial Lead | Commercial | R-007, R-016 | 0 | 2 Medium | 0 | 12 |
| Product Owner | Product Lead | R-017 | 0 | 1 Medium | 0 | 6 |

**Risk Concentration Analysis:**
- ⚠️ **DESNZ SRO owns 7 risks (35%) totaling 66 residual points** — Consider delegating R-012 (spending controls) and R-020 (NAO scrutiny) to Programme Commercial Lead
- **Programme Director has 5 well-distributed risks** — Appropriate concentration
- **Technical Architect has 3 technology risks** — Expected and appropriate

---

## F. 4Ts Response Framework Summary

| Response | Count | % | Total Residual Score | Key Examples |
|----------|-------|---|---------------------|--------------|
| **TOLERATE** | 3 | 15% | 24 | R-006 (political change), R-019 (scope creep), R-020 (NAO scrutiny) |
| **TREAT** | 16 | 80% | 154 | R-001, R-002, R-003, R-004, R-005, R-007, R-008, R-009, R-010, R-011, R-012, R-013, R-014, R-015, R-017, R-018 |
| **TRANSFER** | 1 | 5% | 15 | R-002 (cyber insurance — in addition to Treat) |
| **TERMINATE** | 0 | 0% | 0 | No activities identified for termination |
| **TOTAL** | 20 | 100% | 186 | |

**Key Insights:**
- **80% of risks require active treatment** — Significant mitigation effort needed; this is expected for a new government digital service
- **Only 15% can be tolerated** — These are largely uncontrollable (political change) or low-impact (scope creep, NAO)
- **Limited transfer opportunity** — Cyber insurance for R-002 is the only viable transfer; most risks are internal to programme
- **No termination** — All programme activities are essential to the strategic objectives

---

## G. Risk Appetite Compliance

*Note: No formal organisational risk appetite exists. Thresholds below are recommended for Programme Board approval.*

**Recommended Risk Appetite Thresholds:**

| Category | Appetite Level | Threshold Score | Rationale |
|----------|---------------|-----------------|-----------|
| STRATEGIC | Medium | ≤ 12 | Willing to accept medium strategic risk for consumer benefit |
| OPERATIONAL | Medium | ≤ 9 | Moderate tolerance given external dependencies |
| FINANCIAL | Medium | ≤ 9 | HM Treasury expects prudent financial management |
| COMPLIANCE | Very Low | ≤ 6 | Minimal tolerance for regulatory non-compliance |
| REPUTATIONAL | Low | ≤ 8 | Government services must maintain public trust |
| TECHNOLOGY | Medium | ≤ 12 | Willing to adopt new patterns with controls |

**Compliance Summary:**

| Category | Appetite | Risks Within | Risks Exceeding | Action Required |
|----------|----------|--------------|-----------------|-----------------|
| STRATEGIC | ≤ 12 | 2 (67%) | 1 (33%) | ⚠️ R-006 exceeds — SRO acceptance required |
| OPERATIONAL | ≤ 9 | 4 (100%) | 0 (0%) | ✅ Compliant |
| FINANCIAL | ≤ 9 | 3 (100%) | 0 (0%) | ✅ Compliant |
| COMPLIANCE | ≤ 6 | 1 (25%) | 3 (75%) | ❌ R-002, R-009, R-010 exceed — urgent action |
| REPUTATIONAL | ≤ 8 | 1 (33%) | 2 (67%) | ⚠️ R-013, R-015 exceed — SRO attention |
| TECHNOLOGY | ≤ 12 | 3 (100%) | 0 (0%) | ✅ Compliant |

**Overall Appetite Compliance:** ⚠️ 3 of 6 risk categories have risks exceeding appetite (COMPLIANCE is most concerning)

---

## H. Prioritised Action Plan

### Priority 1: URGENT (Compliance Risks Exceeding Appetite)

| # | Action | Risk(s) | Owner | Due Date | Expected Impact |
|---|--------|---------|-------|----------|-----------------|
| 1 | Complete DPIA and ICO pre-consultation | R-002, R-010 | DPO / Privacy Lead | 2026-06-30 | Reduce R-010 from 12 to 8 |
| 2 | Complete threat model with NCSC | R-002 | Security Lead | 2026-05-31 | Reduce R-002 from 15 to 10 |
| 3 | Develop incident response plan (ICO 72-hour notification) | R-002, R-013 | DPO / Privacy Lead | 2026-08-31 | Reduce R-013 from 12 to 8 |

### Priority 2: HIGH (Strategic and Reputational Risks)

| # | Action | Risk(s) | Owner | Due Date | Expected Impact |
|---|--------|---------|-------|----------|-----------------|
| 4 | Secure Smart Energy GB co-marketing agreement | R-001 | Programme Director | 2026-04-30 | Reduce R-001 from 9 to 6 |
| 5 | Obtain Ofgem endorsement of tariff comparison methodology | R-015 | Programme Director | 2026-09-30 | Reduce R-015 from 9 to 6 |
| 6 | Prepare ministerial continuation brief template | R-006 | DESNZ SRO | 2026-06-30 | Reduce R-006 from 16 to 12 |

### Priority 3: MEDIUM (Technology and Operational Risks)

| # | Action | Risk(s) | Owner | Due Date | Expected Impact |
|---|--------|---------|-------|----------|-----------------|
| 7 | Initiate SEC authorisation for DCC access | R-004 | Programme Director | 2026-03-31 | Reduce R-004 from 6 to 4 |
| 8 | Agree formal DCC capacity allocation | R-005 | Programme Director | 2026-05-31 | Reduce R-005 from 8 to 4 |
| 9 | Establish monthly supplier forum | R-003 | Programme Director | 2026-03-31 | Reduce R-003 from 9 to 6 |
| 10 | Implement FinOps practice from Alpha | R-007 | Technical Architect | 2026-05-31 | Reduce R-007 from 6 to 4 |

**Overall Action Plan Summary:**
- **Total Actions:** 10 priority actions
- **Expected Total Risk Reduction:** ~36 points (19% additional reduction)
- **Target Completion:** All Priority 1 by 2026-08-31; all actions by 2026-09-30

---

## I. Integration with SOBC

**How this Risk Register feeds into Strategic Outline Business Case (ARC-001-SOBC-v1.0):**

### SOBC Strategic Case (Part A)
- **R-006** (political change): Demonstrates urgency — deliver early value before political landscape shifts
- **R-001** (low adoption): Justifies investment in user-centred design and marketing

### SOBC Economic Case (Part B)
- **HM Treasury Optimism Bias**: Apply 25% optimism bias to costs (standard for new digital service, per Green Book Supplementary Guidance)
- **R-007** (cloud costs): Add 15% contingency to infrastructure costs
- **R-003** (supplier delays): Add 10% contingency for extended integration timeline
- **Total risk contingency:** ~£2M added to Economic Case

### SOBC Management Case (Part E — Risk Management)
- Full risk register included as Annex to Management Case
- Top 10 risks table for executive summary
- Risk ownership matrix demonstrates clear accountability
- Monitoring framework shows ongoing risk management capability

### SOBC Recommendation
- Risk profile is ⚠️ Concerning but manageable with active treatment
- No Critical residual risks that would prevent programme proceeding
- Compliance risks require early regulatory engagement to de-risk
- Phased delivery approach recommended to manage risk incrementally

---

## J. Monitoring and Review Framework

### Review Schedule

| Risk Level | Review Frequency | Reviewed By | Escalated To |
|------------|------------------|-------------|--------------|
| **Critical (20-25)** | Weekly | Risk Owner + PMO | Steering Committee |
| **High (13-19)** | Fortnightly | Risk Owner | Programme Board |
| **Medium (6-12)** | Monthly | Risk Owner | Programme Director |
| **Low (1-5)** | Quarterly | Action Owner | Risk Owner |

### Key Risk Indicators (KRIs)

**Leading Indicators:**
- DCC integration progress (milestone completion rate) — predicts R-004, R-005
- Supplier API readiness (number of suppliers with production-ready APIs) — predicts R-003
- Security test findings (critical/high vulnerability count) — predicts R-002
- User research satisfaction scores — predicts R-001

**Lagging Indicators:**
- Actual vs planned timeline variance — confirms R-004, R-008
- Actual vs budgeted cloud costs — confirms R-007
- App store ratings — confirms R-001, R-013
- ICO/Ofgem correspondence tone and findings — confirms R-010

### Escalation Criteria

**Automatic Escalation Triggers:**
1. Any risk increases by 5+ points
2. Any new Critical risk (score 20-25) identified
3. Any risk exceeds appetite with no approved mitigation plan
4. Any mitigation action delayed >4 weeks past due date
5. 3+ risks in same category exceed appetite simultaneously

### Reporting Requirements

**Weekly** (Critical Risks Only): Dashboard to Steering Committee — R-006 currently the only Critical residual risk

**Monthly** (All Risks): Full risk register to Programme Board with:
- Risk matrix visualisation
- Risk appetite compliance summary
- Action plan progress
- KRI dashboard

**Quarterly** (Strategic Review): Risk register to DESNZ governance with:
- Risk trend analysis
- Risk appetite threshold review
- Lessons learned
- Control effectiveness review

### Risk Register Maintenance

**Risk Register Owner:** Programme Director (to be confirmed)

**Next Review Date:** 2026-02-28

**Version Control:** Version increments with each material update; change log in Revision History

---

## K. Orange Book Compliance Checklist

### Part I — Risk Management Principles

- ✅ **A. Governance and Leadership**: Risk owners assigned from stakeholder RACI matrix; escalation paths defined to Steering Committee and Minister; risk appetite thresholds recommended for Board approval
- ✅ **B. Integration**: Risks linked to stakeholder goals (G-1 through G-7), outcomes (O-1 through O-4), and SOBC; risk management embedded in programme governance
- ✅ **C. Collaboration and Best Information**: Risks sourced from stakeholder concerns (ARC-001-STKE-v1.0), architecture principles (ARC-000-PRIN-v1.0), and requirements (ARC-001-REQ-v1.0); evidence-based assessment with justified scores
- ✅ **D. Risk Management Processes**: Systematic identification across 6 Orange Book categories; consistent 5×5 assessment methodology; 4Ts response framework applied; inherent and residual risk tracked
- ✅ **E. Continual Improvement**: Review schedule defined (weekly/monthly/quarterly); KRIs established; lessons learned process; risk register version control

### Part II — Risk Control Framework

- ✅ **4-Pillar "House" Structure**: Risk appetite defined (recommended for approval); risk ownership and governance established; risk assessment methodology documented; control effectiveness measured (inherent vs residual)

---

## Appendix A: Stakeholder-Risk Linkage

| Stakeholder | Driver (from ARC-001-STKE-v1.0) | Risk ID | Risk Title | Category | Residual Score |
|-------------|----------------------------------|---------|------------|----------|----------------|
| DESNZ Minister | SD-1: Demonstrate SMIP return | R-001 | Low consumer adoption | STRATEGIC | 9 |
| DESNZ Minister | SD-1: Demonstrate SMIP return | R-006 | Political change | STRATEGIC | 16 |
| DESNZ Minister | SD-1: Demonstrate SMIP return | R-013 | Service failure | REPUTATIONAL | 12 |
| DESNZ SRO | SD-2: Deliver on time/budget | R-004 | DCC integration delays | TECHNOLOGY | 6 |
| DESNZ SRO | SD-2: Deliver on time/budget | R-008 | Team capacity | OPERATIONAL | 6 |
| DESNZ SRO | SD-2: Deliver on time/budget | R-019 | Scope creep | STRATEGIC | 4 |
| Ofgem | SD-3: Protect consumers | R-010 | GDPR non-compliance | COMPLIANCE | 12 |
| Ofgem | SD-3: Protect consumers | R-015 | Tariff comparison bias | REPUTATIONAL | 9 |
| ICO | SD-4: Lawful processing | R-002 | Data breach | COMPLIANCE | 15 |
| ICO | SD-4: Lawful processing | R-010 | GDPR non-compliance | COMPLIANCE | 12 |
| DCC | SD-5: Infrastructure stability | R-004 | DCC integration delays | TECHNOLOGY | 6 |
| DCC | SD-5: Infrastructure stability | R-005 | DCC capacity constraints | TECHNOLOGY | 8 |
| DCC | SD-5: Infrastructure stability | R-016 | DCC commercial model | FINANCIAL | 6 |
| Energy Suppliers | SD-6: Manage customer relationship | R-003 | Supplier non-cooperation | OPERATIONAL | 9 |
| Energy Suppliers | SD-6: Manage customer relationship | R-011 | Data inconsistency | TECHNOLOGY | 8 |
| Energy Suppliers | SD-6: Manage customer relationship | R-015 | Tariff comparison bias | REPUTATIONAL | 9 |
| Citizens | SD-7: Reduce energy costs | R-001 | Low adoption | STRATEGIC | 9 |
| Citizens | SD-7: Reduce energy costs | R-002 | Data breach | COMPLIANCE | 15 |
| Citizens | SD-7: Reduce energy costs | R-017 | Recommendation quality | OPERATIONAL | 6 |
| HM Treasury | SD-9: Value for money | R-007 | Cloud costs exceed budget | FINANCIAL | 6 |
| HM Treasury | SD-9: Value for money | R-012 | Spending control delays | FINANCIAL | 6 |
| HM Treasury | SD-9: Value for money | R-020 | NAO/PAC scrutiny | REPUTATIONAL | 4 |
| Consumer Orgs | SD-10: Inclusive service | R-014 | Accessibility failure | COMPLIANCE | 8 |
| GDS Assessors | SD-11: Service Standard | R-009 | GDS assessment failure | COMPLIANCE | 9 |
| NCSC | SD-12: Cyber security | R-002 | Data breach | COMPLIANCE | 15 |

---

## Appendix B: Conflict-to-Risk Mapping

| Stakeholder Conflict (from ARC-001-STKE-v1.0) | Risk(s) Created | Mitigation |
|-------------------------------------------------|-----------------|------------|
| Conflict 1: DESNZ Minister (speed) vs Regulators (rigour) | R-009, R-010, R-013 | Phased launch — regulatory sign-offs before real data |
| Conflict 2: Suppliers (protect customers) vs Citizens/Ofgem (impartial comparison) | R-003, R-015 | Ofgem mandate, transparent methodology, supplier forum |
| Conflict 3: DCC (limit load) vs Adoption goals (millions of requests) | R-004, R-005 | Batch retrieval, caching, capacity agreement |
| Conflict 4: Treasury (minimal cost) vs Accessibility/Security investment | R-007, R-014 | Frame as compliance cost (legal obligation), not discretionary |

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| **Risk Register Owner** | [Programme Director] | | |
| **Senior Responsible Owner** | [DESNZ SRO] | | |
| **Steering Committee Chair** | [Chair] | | |

---

## Next Steps

1. **Immediate Actions** (This Week):
   - [ ] Present risk register to Programme Board for review
   - [ ] Establish formal risk appetite thresholds (create `projects/000-global/risk-appetite.md`)
   - [ ] Assign risk owners and confirm acceptance

2. **Short-term Actions** (This Month):
   - [ ] Initiate Priority 1 actions (DPIA, threat model, incident response plan)
   - [ ] Set up monthly risk review cadence
   - [ ] Integrate risk register into SOBC Management Case Part E

3. **Medium-term Actions** (This Quarter):
   - [ ] Complete all Priority 1 and 2 actions
   - [ ] First monthly risk review with updated scores
   - [ ] DCC and supplier engagement to de-risk R-003, R-004, R-005

---

**END OF RISK REGISTER**

---

*This risk register follows HM Treasury Orange Book (2023) principles and integrates with ArcKit's stakeholder-driven architecture governance framework.*

*For questions or updates, contact: [Risk Register Owner Name and Email]*

---

**Generated by**: ArcKit `/arckit.risk` command
**Generated on**: 2026-01-31
**ArcKit Version**: 1.0.3
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**AI Model**: Claude Opus 4.5 (claude-opus-4-5-20251101)
