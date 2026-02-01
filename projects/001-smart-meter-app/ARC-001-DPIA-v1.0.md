# Data Protection Impact Assessment (DPIA)

> **Template Status**: Beta | **Version**: 1.0.0 | **Command**: `/arckit.dpia`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-DPIA-v1.0 |
| **Document Type** | Data Protection Impact Assessment |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | DESNZ SRO, DPO/Privacy Lead, ICO (if consulted), CDDO, Security Lead |
| **Project Name** | UK Smart Meter Data Consumer Mobile App |
| **Assessment Date** | 2026-02-01 |
| **Data Protection Officer** | DPO/Privacy Lead (to be appointed) |
| **Data Controller** | Department for Energy Security and Net Zero (DESNZ) |
| **Author** | Enterprise Architect |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-02-01 | ArcKit AI | Initial creation from `/arckit.dpia` command | PENDING | PENDING |

## Executive Summary

**Processing Activity**: Collection, storage, analysis, and presentation of half-hourly smart meter energy consumption data (gas and electricity) for approximately 34 million UK households via a cross-platform mobile application.

**DPIA Outcome**: MEDIUM residual risk to data subjects

**Approval Status**: PENDING

**Key Findings**:
- Processing meets 4 of 9 ICO screening criteria, making a DPIA mandatory under UK GDPR Article 35
- Energy consumption data, while not special category data under Article 9, is behaviourally sensitive — it can reveal household occupancy patterns, daily routines, appliance usage, and lifestyle indicators
- 34 million potential data subjects include vulnerable groups (elderly, digitally cautious, prepayment meter users on low incomes, disabled users)
- Granular consent management with 4 distinct purposes provides strong data subject control
- All residual risks can be reduced to MEDIUM or LOW with planned technical and organisational measures
- No international data transfers — all data processed and stored within UK data centres

**Recommendation**: Proceed with conditions

**ICO Consultation Required**: NO (all residual risks are MEDIUM or LOW after mitigation)

---

## 1. DPIA Screening Assessment

### 1.1 Screening Criteria (ICO's 9 Criteria)

| # | Criterion | YES/NO | Evidence |
|---|-----------|--------|----------|
| 1 | **Evaluation or scoring** including profiling and predicting | **YES** | FR-006: Personalised energy-saving recommendations use consumption pattern analysis to evaluate household behaviour and predict savings opportunities. FR-007: Tariff comparison uses actual half-hourly consumption data to score and rank tariff suitability. |
| 2 | **Automated decision-making with legal or similarly significant effect** | **NO** | Recommendations (FR-006) and tariff comparisons (FR-007) are informational only. No automated decisions produce legal effects or similarly significant effects on data subjects. Users retain full control over energy supplier switching and behaviour changes. |
| 3 | **Systematic monitoring** of data subjects | **YES** | FR-001/FR-002: Continuous collection of half-hourly electricity and gas meter readings via DCC infrastructure and energy supplier APIs. This constitutes systematic monitoring of household energy consumption over time, revealing occupancy patterns and daily routines. |
| 4 | **Sensitive data or data of highly personal nature** | **NO** | No special category data (Article 9) is processed. No health, biometric, genetic, racial, political, religious, trade union, sex life, or criminal offence data. Energy consumption data is behaviourally revealing but does not meet the Article 9 threshold. |
| 5 | **Processing on a large scale** | **YES** | 34 million smart meter households (data subjects). Projected 150 billion consumption readings by Year 3 (~50TB). National geographic scope across England, Scotland, and Wales. Continuous processing over multi-year retention periods. |
| 6 | **Matching or combining datasets** from different sources | **NO** | While data is sourced from DCC, energy suppliers (Octopus, n3rgy), National Grid ESO (carbon intensity), and tariff comparison providers, the combination is reasonably expected by data subjects who sign up for an energy monitoring app. Data subjects explicitly consent to each data source connection. |
| 7 | **Data concerning vulnerable data subjects** | **YES** | Stakeholder analysis identifies: (a) Margaret persona — 68-year-old digitally cautious pensioner on a prepayment meter with limited income; (b) Aisha persona — visually impaired user requiring assistive technology; (c) Prepayment meter users — disproportionately low-income and fuel-poor households; (d) Elderly users — potentially digitally excluded. |
| 8 | **Innovative use or application of new technological or organisational solutions** | **NO** | Standard mobile app architecture (React Native/Flutter), established time-series database (TimescaleDB), standard REST/GraphQL APIs, established authentication (GOV.UK One Login). No AI/ML, blockchain, IoT sensors, biometrics, or novel technology. |
| 9 | **Processing that prevents data subjects from exercising a right or using a service/contract** | **NO** | Full data subject rights implemented: SAR endpoint (FR-015), granular consent withdrawal (FR-003, UC-7), account deletion with data erasure (UC-8), data portability export in JSON/CSV (FR-010). Consent refusal for optional purposes does not prevent core service access. |

**Screening Score**: 4/9 criteria met

### 1.2 DPIA Necessity Decision

**Decision**: DPIA REQUIRED

**Rationale**:
- 4 of 9 ICO criteria are met (≥2 triggers mandatory DPIA)
- Large-scale systematic monitoring of energy consumption for 34 million households
- Evaluation and profiling through personalised energy recommendations
- Processing involves vulnerable data subjects including elderly, disabled, and fuel-poor households
- Data model entity E-004 (Consumption Reading) explicitly states GDPR status as NEEDS_DPIA
- Secure by Design assessment (ARC-001-SECD-v1.0) identifies DPIA as a CRITICAL gap
- Risk register R-010 identifies DPIA completion as a required action

**Decision Authority**: DPO/Privacy Lead (to be appointed)

**Decision Date**: PENDING (this assessment provides the evidence base)

---

## 2. Description of Processing

### 2.1 Nature of Processing

**What operations are being performed?**
- [x] Collection — Half-hourly meter readings from DCC and energy supplier APIs
- [x] Recording — Consumption data stored in TimescaleDB time-series database
- [x] Organisation — Data structured by meter, time period, tariff, and consumption type
- [x] Structuring — Aggregation into daily, weekly, monthly, and annual summaries
- [x] Storage — Persistent storage with hot/warm/cold tiering strategy
- [x] Adaptation/alteration — Unit conversion (kWh to cost), carbon footprint calculation
- [x] Retrieval — On-demand access via mobile app and SAR endpoint
- [x] Consultation — Pattern analysis for energy-saving recommendations
- [x] Use — Tariff comparison, budget tracking, consumption alerts
- [ ] Disclosure by transmission — No third-party disclosure beyond data processors
- [ ] Dissemination — No public disclosure of personal data
- [x] Alignment/combination — Combining meter readings with tariff data and carbon intensity
- [x] Restriction — Consent-based processing restriction per purpose
- [x] Erasure/destruction — Account deletion with full data erasure within 30 days

**Processing Method**:
- [x] Automated processing
- [ ] Manual processing
- [ ] Combination of automated and manual

**Profiling Involved**: YES
- Personalised energy-saving recommendations (FR-006) analyse consumption patterns to identify savings opportunities. This constitutes profiling under UK GDPR Article 4(4) as it evaluates personal aspects relating to household behaviour. However, recommendations are purely informational with no legal or similarly significant effect.

**Automated Decision-Making**: NO
- All recommendations and comparisons are advisory. No automated decisions produce legal effects or similarly significant effects. Users make all decisions about energy supplier switching, behaviour changes, and budget management.

### 2.2 Scope of Processing

#### What data are we processing?

**Personal Data Categories** (from Data Model ARC-001-DATA-v1.0):

| Entity ID | Entity Name | Data Categories | Special Category? | PII Level |
|-----------|-------------|-----------------|-------------------|-----------|
| E-001 | Consumer Profile | email, display_name, locale, timezone, accessibility_preferences | NO | HIGH (direct identifiers) |
| E-002 | Linked Meter | mpan, mprn, meter_serial, fuel_type, supplier_name | NO | HIGH (unique meter identifiers linkable to address) |
| E-003 | Tariff Plan | supplier, plan_name, rates, standing_charge | NO | LOW (contractual data) |
| E-004 | Consumption Reading | meter_id, timestamp, value_kwh, quality_flag | NO | MEDIUM (indirect PII — reveals household behaviour) |
| E-005 | Budget | target_amount, period, alert_threshold | NO | LOW (user preferences) |
| E-006 | Consumption Alert | alert_type, threshold, delivery_channel | NO | LOW (notification preferences) |
| E-007 | Recommendation | type, title, estimated_saving, consumption_pattern_ref | NO | LOW (system-generated advice) |
| E-008 | Tariff Comparison | current_tariff, compared_tariff, projected_saving | NO | LOW (calculated comparison) |
| E-009 | Carbon Footprint | emission_factor, total_kg_co2 | NO | LOW (calculated metric) |
| E-010 | Consent Record | purpose, status, granted_at, withdrawn_at, version | NO | MEDIUM (legal record of consent) |
| E-011 | Feedback | type, rating, description | NO | LOW (may contain PII in free text) |
| E-012 | Audit Log | action, entity_type, ip_address, user_agent | NO | MEDIUM (activity tracking) |

**Total Data Items**: 108 personal data attributes across 12 entities

**Special Category Data**: NO — No Article 9 data is processed

**Children's Data**: NO — Service is for energy bill payers (adults). Account registration requires being the named account holder or authorised representative for a smart meter installation.

#### Whose data are we processing?

**Data Subject Categories** (from Stakeholder Analysis ARC-001-STKE-v1.0):

| Data Subject Type | Description | Volume | Vulnerable? |
|-------------------|-------------|--------|-------------|
| Smart meter householders | UK residents with SMETS1/SMETS2 smart meters who register for the app | Up to 34 million | Some |
| Elderly/digitally cautious users | Pensioners and older adults with limited digital confidence (Margaret persona) | Estimated 5-8 million | YES |
| Prepayment meter users | Households on prepayment tariffs, disproportionately low-income | Estimated 4 million | YES |
| Disabled users | Users requiring assistive technology (Aisha persona — visual impairment) | Estimated 2-3 million | YES |

**Total Data Subjects**: Up to 34 million individuals (UK smart meter households)

**Vulnerable Groups**: Elderly users with limited digital literacy, prepayment meter users on low incomes (fuel poverty), disabled users requiring accessible interfaces

#### How much data?

**Volume Metrics**:
- **Records**: 150 billion consumption readings projected by Year 3
- **Data subjects**: Up to 34 million individuals
- **Storage size**: ~50TB projected by Year 3
- **Transaction rate**: ~2 billion new readings per month at full scale (34M meters × ~1,440 readings/month each)
- **Geographic scope**: UK-wide (England, Scotland, Wales — following DCC coverage)

**Scale Classification**: Large scale
- 34 million data subjects (national population scale)
- 150 billion individual data records
- UK-wide geographic scope
- Continuous processing over multi-year periods

#### How long are we keeping it?

**Retention Periods** (from Data Model ARC-001-DATA-v1.0):

| Data Type | Retention Period | Legal Basis for Retention | Deletion Method |
|-----------|------------------|---------------------------|-----------------|
| Consumer Profile (E-001) | Account lifetime + 12 months | Contract (Article 6(1)(b)) | Secure deletion with cryptographic erasure |
| Linked Meter (E-002) | Account lifetime + 12 months | Contract (Article 6(1)(b)) | Secure deletion |
| Consumption Readings (E-004) | Hot: 90 days, Warm: 2 years, Cold: 5 years | Consent (Article 6(1)(a)) | Automated tiered deletion, anonymisation for cold tier |
| Consent Records (E-010) | 7 years from last action | Legal obligation (Article 6(1)(c)) — accountability | Secure deletion after retention period |
| Audit Logs (E-012) | 7 years | Legal obligation (Article 6(1)(c)) — regulatory compliance | Secure deletion after retention period |
| Feedback (E-011) | Account lifetime + 12 months | Legitimate interests | Anonymisation or secure deletion |

**Maximum Retention**: 7 years (consent records and audit logs for legal accountability)

**Automated Deletion**: YES — Automated retention enforcement with tiered storage lifecycle management. Consumption readings automatically move from hot (90 days) to warm (2 years) to cold (5 years) tiers with progressive aggregation and eventual anonymisation.

### 2.3 Context of Processing

#### Why are we processing this data?

**Processing Purpose** (from Requirements ARC-001-REQ-v1.0):

| Requirement ID | Purpose | Stakeholder Goal |
|----------------|---------|------------------|
| BR-001 | Enable citizens to view their energy consumption data | Citizen empowerment and transparency (SD-7) |
| BR-002 | Provide actionable energy-saving insights | Reduce household energy bills and carbon emissions (SD-1, SD-7) |
| BR-003 | Enable informed tariff switching decisions | Consumer choice and market competition (SD-3, SD-7) |
| BR-004 | Support net zero carbon reduction targets | DESNZ policy delivery (SD-1) |
| FR-003 | Granular consent management for data processing | ICO compliance, data subject control (SD-4) |
| FR-006 | Personalised energy-saving recommendations | Behavioural insights for energy reduction (SD-7) |
| FR-007 | Tariff comparison using actual consumption | Informed switching decisions (SD-3, SD-7) |
| DR-001 | Half-hourly consumption data collection and storage | Core service delivery |
| DR-003 | Data quality and validation | Accurate insights and recommendations |
| DR-005 | Data portability and export | Data subject rights (Article 20) |

**Primary Purpose**: Empower UK smart meter consumers to understand, manage, and reduce their energy consumption through transparent access to their half-hourly meter data, personalised recommendations, and tariff comparison tools.

**Secondary Purposes**: (a) Support UK net zero policy objectives through aggregate behavioural insights; (b) Enable regulatory reporting by Ofgem on smart meter programme effectiveness (using anonymised/aggregated data only).

#### What is the relationship with data subjects?

**Relationship Type**:
- [x] Citizen/public service user

**Power Balance**:
- [x] Imbalanced relationship (government-citizen)
- Safeguards: Granular consent with 4 distinct purposes (viewing, recommendations, tariff comparison, research). Consent withdrawal does not affect core account access. Full data portability and deletion rights. Independent ICO oversight. DPO appointed with direct reporting line. Accessible complaints mechanism.

#### How much control do data subjects have?

**Control Mechanisms**:
- [x] Consent can be withdrawn — Per-purpose withdrawal via in-app consent management (FR-003, UC-7)
- [x] Can opt out of processing — Optional purposes (recommendations, tariff comparison, research) can be individually declined
- [x] Can access their data (Subject Access Request) — SAR endpoint with structured data export (FR-015)
- [x] Can correct inaccurate data (rectification) — Account settings allow profile data correction
- [x] Can request deletion (right to erasure) — Account deletion with full data erasure within 30 days (UC-8)
- [x] Can object to processing — Objection mechanism for each processing purpose
- [x] Can request restriction of processing — Purpose-level restriction via consent management
- [x] Can port data to another controller — JSON and CSV export of consumption data (FR-010)
- [x] Can object to automated decisions — N/A (no solely automated decision-making with legal effect)

**Limitations on Control**: Consent records and audit logs are retained for 7 years after account deletion under legal obligation (Article 6(1)(c)) for regulatory accountability. Data subjects cannot request deletion of these records during the retention period.

#### Would data subjects expect this processing?

**Reasonable Expectation Assessment**:
- **Transparency**: YES — Privacy notice presented at registration, consent purposes explained in plain English
- **Privacy Notice**: YES — Clear privacy notice compliant with Articles 13/14, available in-app and on web
- **Expectation**: YES — Users who download and register for an energy monitoring app would reasonably expect their meter data to be collected, stored, and used to provide consumption insights, recommendations, and comparisons

**If unexpected processing**: The secondary purpose of anonymised/aggregated data for policy research is disclosed in the privacy notice but may be less expected. Mitigation: This is an optional consent purpose ("research") that can be independently declined without affecting service access.

### 2.4 Purpose and Benefits

#### What do we want to achieve?

**Intended Outcomes** (from Stakeholder Goals):

| Stakeholder Goal | Processing Contribution | Measurable Benefit |
|------------------|------------------------|-------------------|
| SD-1: DESNZ Net Zero delivery | Aggregate consumption reduction through behavioural nudges | 5-15% household energy reduction |
| SD-3: Ofgem market competition | Tariff comparison using actual usage data | Increased switching rates, £100-300 annual savings per household |
| SD-7: Citizen empowerment | Transparent access to own energy data | 34 million households able to view and understand their consumption |
| SD-8: Smart Energy GB engagement | Digital channel for smart meter benefits | Increased smart meter satisfaction and usage |
| SD-10: Accessibility for all | WCAG 2.2 AA compliant, assistive technology support | Inclusive access for disabled and digitally excluded users |

**Primary Benefit**: Empowering citizens to reduce energy consumption and costs through data-driven insights, supporting UK net zero targets.

#### Who benefits?

- [x] Data subjects: Reduced energy bills (£100-300/year), carbon footprint visibility, informed tariff switching, personalised savings recommendations
- [x] Organisation: DESNZ delivers smart meter policy objectives, demonstrates citizen-centric digital service
- [x] Society/public: Contribution to UK net zero targets, reduced national energy demand, improved energy market competition
- [ ] Third parties: N/A

---

## 3. Consultation

### 3.1 Data Protection Officer (DPO) Consultation

**DPO Name**: To be appointed (identified as CRITICAL gap in ARC-001-SECD-v1.0)

**Date Consulted**: PENDING

**DPO Advice**: PENDING — DPO must be appointed before processing commences. This DPIA provides the evidence base for DPO review.

**DPO Recommendations**: PENDING

**How DPO Advice Addressed**: Will be documented upon DPO appointment and review.

### 3.2 Data Subject Consultation

**Consultation Method**:
- [ ] Not consulted yet (explain why: Project is at pre-Alpha architecture stage. Data subject consultation is planned for Alpha phase through GDS user research activities.)

**Planned Consultation**:
- User research with representative sample including Margaret (elderly, prepayment) and Aisha (visually impaired) personas during Alpha
- Usability testing of consent management flows
- Privacy notice comprehension testing with vulnerable user groups
- Public beta feedback mechanism for privacy concerns

**Date(s) Consulted**: PLANNED for Alpha phase (estimated Q3 2026)

### 3.3 Stakeholder Consultation

**Stakeholders Consulted** (from Stakeholder RACI):

| Stakeholder | Role | Date Consulted | Feedback Summary |
|-------------|------|----------------|------------------|
| DESNZ SRO | Data Controller representative | PENDING | To review DPIA before approval |
| ICO | Supervisory authority | PENDING | Prior consultation not required (residual risks MEDIUM or below) |
| Ofgem | Regulator (energy) | PENDING | To advise on SEC data access obligations |
| DCC | Data processor (meter infrastructure) | PENDING | To confirm data processing arrangements and DPA |
| NCSC | Security advisor | PENDING | Secure by Design assessment completed (ARC-001-SECD-v1.0) |
| GDS/CDDO | Standards authority | PENDING | Service assessment will review DPIA as Point 5 evidence |

**Key Stakeholder Concerns**: To be captured during consultation round.

---

## 4. Necessity and Proportionality Assessment

### 4.1 Lawful Basis Assessment

**Lawful Bases** (multiple bases apply to different processing activities):

- [x] **(a) Consent** — Data subject has given clear consent for processing for a specific purpose
  - **Applies to**: Consumption data viewing (E-004), personalised recommendations (E-007), tariff comparison (E-008), research purposes
  - Evidence of consent: Granular consent management (FR-003) with 4 distinct purposes, each independently controllable
  - Freely given, specific, informed, unambiguous: YES — Consent is granular (4 purposes), not bundled with service access, plain English explanations, affirmative opt-in
  - Withdrawal mechanism: In-app consent management (UC-7) with immediate effect; withdrawal of optional purposes does not affect core account

- [x] **(b) Contract** — Processing is necessary to perform a contract with the data subject
  - **Applies to**: Account creation and management (E-001), meter linking (E-002), tariff plan storage (E-003)
  - Contract type: Terms of Service for app usage
  - How processing is necessary: Account credentials and linked meter identifiers are essential to deliver the contracted service

- [x] **(c) Legal obligation** — Processing is necessary to comply with the law
  - **Applies to**: Consent records (E-010), audit logs (E-012)
  - Legal obligation: UK GDPR Article 5(2) accountability principle; Article 7(1) demonstration of consent; ICO enforcement cooperation
  - Compliance requirement: Must maintain auditable records of consent grants, withdrawals, and data processing activities for 7 years

**Justification for Chosen Bases**: Multiple lawful bases are applied on a purpose-by-purpose basis following ICO guidance. Consent is used for the core energy data processing as it provides the strongest data subject control for behaviourally sensitive data. Contract is used for account management essentials. Legal obligation is used for accountability records that cannot be subject to erasure requests.

### 4.2 Special Category Data Basis (Article 9)

**Applicable**: NO

No special category data is processed. Energy consumption data, while behaviourally sensitive, does not fall within any Article 9 category.

### 4.3 Necessity Assessment

**Is processing necessary to achieve the purpose?**

| Question | Answer | Justification |
|----------|--------|---------------|
| Can we achieve the purpose without processing personal data? | NO | Energy consumption data is inherently personal — it relates to a specific household's meter. Anonymised data cannot provide individual consumption insights, personalised recommendations, or tariff comparisons. |
| Can we achieve the purpose with less personal data? | NO | Half-hourly granularity is the minimum resolution for meaningful energy insights and accurate tariff comparison. Coarser data (daily/monthly) would not support time-of-use tariff analysis or peak/off-peak usage patterns. Display name and email are minimum identifiers. |
| Can we achieve the purpose with less intrusive processing? | NO | Direct meter data collection via DCC/supplier APIs is the least intrusive method — it avoids manual data entry, physical meter reading visits, or integration with more sensitive data sources (e.g., bank transactions). |
| Can we achieve the purpose by processing data for less time? | PARTIALLY | Hot tier (90 days) covers immediate monitoring. Warm tier (2 years) is necessary for year-on-year comparison. Cold tier (5 years) could potentially be reduced; however, long-term trend analysis and tariff comparison accuracy improve with historical data. Retention is proportionate given user control over deletion. |

**Necessity Conclusion**: Processing is NECESSARY

**Alternatives Considered**:
1. **Aggregate/anonymised data only** — Rejected because: Individual consumption insights, personalised recommendations, and tariff comparison require individual-level data
2. **Daily rather than half-hourly granularity** — Rejected because: Time-of-use tariffs, peak/off-peak analysis, and meaningful energy-saving recommendations require half-hourly resolution
3. **User-entered data instead of API collection** — Rejected because: Manual entry is burdensome, error-prone, and would exclude digitally cautious users; automated collection via DCC/APIs is more accurate and accessible

### 4.4 Proportionality Assessment

**Is the processing proportionate to the purpose?**

**Data Minimization**:
- [x] We only collect data that is adequate for the purpose — Each of 108 attributes mapped to specific processing purpose in data model
- [x] We only collect data that is relevant for the purpose — No address, financial, or demographic data collected beyond minimum identifiers
- [x] We do not collect excessive data — No special category data, no social media data, no third-party enrichment beyond disclosed sources

**Proportionality Factors**:

| Factor | Assessment | Score (1-5) |
|--------|------------|-------------|
| Severity of intrusion into private life | Medium — Energy data reveals occupancy patterns and daily routines | 3 |
| Benefits to data subjects | High — Reduced energy bills (£100-300/year), carbon footprint awareness, informed tariff switching | 5 |
| Benefits to organisation | Medium — Policy delivery, service standard compliance | 3 |
| Benefits to society | High — National energy reduction, net zero contribution | 4 |
| Reasonable alternatives exist | No — No less intrusive way to provide personalised energy insights | 1 |

**Proportionality Conclusion**: Processing is PROPORTIONATE

**Justification**: The benefits to data subjects (financial savings, empowerment, reduced energy costs) and society (net zero targets, energy market competition) significantly outweigh the privacy intrusion. Energy consumption data is behaviourally sensitive but not special category. Strong data subject control through granular consent, full rights implementation, and data minimisation ensure proportionality. No less intrusive alternative can achieve the stated purposes.

---

## 5. Risk Assessment to Data Subjects

**CRITICAL**: These are risks to **individuals' rights and freedoms**, NOT organisational risks.

### 5.1 Risk Identification

**Risk Categories Considered**:
- Physical harm (occupancy pattern exposure enabling burglary)
- Material damage (financial loss from inaccurate tariff advice, identity fraud from meter identifier exposure)
- Non-material damage (distress from surveillance perception, loss of control over personal data, embarrassment from consumption pattern disclosure, anxiety for vulnerable users)

### 5.2 Inherent Risks (Before Mitigation)

| Risk ID | Risk Description | Impact on Data Subjects | Likelihood | Severity | Risk Level | Risk Source |
|---------|------------------|-------------------------|------------|----------|------------|-------------|
| DPIA-001 | Unauthorised access to consumption data | Household occupancy patterns exposed, enabling targeted burglary or surveillance; distress from privacy violation | Medium | High | **HIGH** | Security vulnerability, insider threat |
| DPIA-002 | Data breach exposing consumer profiles and meter identifiers | Identity fraud using MPAN/MPRN combined with email; phishing attacks targeting energy consumers | Medium | High | **HIGH** | External attack, supply chain compromise |
| DPIA-003 | Inaccurate consumption data leading to wrong recommendations | Financial loss from poor tariff switching advice; incorrect budget alerts causing anxiety; fuel-poor households making wrong decisions | Medium | Medium | **MEDIUM** | Data quality from DCC/supplier APIs |
| DPIA-004 | Consumption pattern analysis revealing sensitive lifestyle information | Inference of household composition, shift work patterns, health-related equipment usage (e.g., oxygen concentrators), religious observance patterns | Low | High | **MEDIUM** | Behavioural inference from energy data |
| DPIA-005 | Excessive data retention beyond necessity | Extended exposure window for breach; data subjects unable to fully disengage; loss of control over personal data | Low | Medium | **LOW** | Retention policy failure, storage lifecycle |
| DPIA-006 | Consent mechanism failures | Processing without valid consent; inability to withdraw consent effectively; vulnerable users not understanding consent choices | Medium | Medium | **MEDIUM** | UI/UX complexity, technical failure |
| DPIA-007 | Disproportionate impact on vulnerable users | Digitally cautious elderly users unable to manage privacy settings; prepayment meter users stigmatised by consumption patterns; disabled users excluded from privacy controls | Medium | High | **HIGH** | Accessibility barriers, digital exclusion |
| DPIA-008 | Function creep — data used for unintended purposes | Energy data shared with third parties for profiling, marketing, credit scoring, or insurance pricing without consent | Low | Very High | **HIGH** | Mission creep, future policy changes |
| DPIA-009 | Re-identification of anonymised/aggregated data | Supposedly anonymised research data re-identified through combination with external datasets, exposing individual consumption | Low | Medium | **LOW** | De-anonymisation attack |
| DPIA-010 | Third-party processor data misuse | DCC, energy supplier, or cloud provider accessing or misusing consumer data beyond contracted purposes | Low | High | **MEDIUM** | Processor non-compliance |

### 5.3 Detailed Risk Analysis

**DPIA-001: Unauthorised Access to Consumption Data**

**Description**: An attacker or malicious insider gains unauthorised access to individual consumption reading data (E-004). Half-hourly readings over time reveal when a household is occupied or vacant, daily routines, and unusual absences.

**Data Subjects Affected**: All registered users (potentially 34 million households)

**Harm to Individuals**:
- Physical: Occupancy pattern data could enable targeted burglary during predicted vacant periods
- Material: Combined with address data (obtainable via MPAN lookup), creates a comprehensive household surveillance dataset
- Non-material: Distress and anxiety from knowing household routines were exposed; feeling of surveillance; loss of trust in government digital services

**Likelihood Analysis**: Medium — The service connects to critical national infrastructure (DCC) and handles data at national scale, making it an attractive target. However, standard security controls significantly reduce likelihood.

**Severity Analysis**: High — Occupancy pattern exposure can facilitate physical harm (burglary). 34 million affected households at scale represents a nationally significant incident.

**Existing Controls**: Security requirements defined in ARC-001-REQ-v1.0 (NFR-SEC-001 through NFR-SEC-006); NCSC Secure by Design assessment completed (ARC-001-SECD-v1.0).

---

**DPIA-007: Disproportionate Impact on Vulnerable Users**

**Description**: Privacy controls, consent management interfaces, and data rights mechanisms are designed for digitally confident users, inadvertently excluding or disadvantaging vulnerable groups identified in the stakeholder analysis.

**Data Subjects Affected**: Estimated 5-8 million elderly users, 4 million prepayment meter users, 2-3 million disabled users

**Harm to Individuals**:
- Physical: None directly
- Material: Vulnerable users may unknowingly consent to processing they don't understand, leading to data exposure
- Non-material: Exclusion from privacy controls; anxiety about data use; feeling of powerlessness; disproportionate impact on those already disadvantaged

**Likelihood Analysis**: Medium — Consent management interfaces are inherently complex. Elderly users (Margaret persona) may struggle with multi-screen consent flows. Visually impaired users (Aisha persona) may face screen reader compatibility issues.

**Severity Analysis**: High — Vulnerable groups are least able to recover from privacy violations and most likely to suffer anxiety and distress. Prepayment meter users on low incomes face disproportionate consequences from any financial harm.

**Existing Controls**: Accessibility requirements (NFR-ACC-001: WCAG 2.2 AA); assistive technology support for Aisha persona; simplified interface for Margaret persona.

---

**DPIA-008: Function Creep — Data Used for Unintended Purposes**

**Description**: Over time, energy consumption data is repurposed beyond the original consent scope — for example, shared with insurers for property risk assessment, used by local authorities for housing inspections, or exploited by energy suppliers for discriminatory pricing.

**Data Subjects Affected**: All registered users

**Harm to Individuals**:
- Physical: None directly
- Material: Discriminatory pricing by energy suppliers or insurers; adverse credit decisions based on consumption patterns; housing enforcement actions based on occupancy inference
- Non-material: Fundamental breach of trust; chilling effect on energy monitoring adoption; disproportionate impact on fuel-poor households

**Likelihood Analysis**: Low — Strong governance controls, granular consent, and purpose limitation principles mitigate this. However, government policy changes over multi-year service lifetime create residual risk.

**Severity Analysis**: Very High — Function creep affecting 34 million households would represent a fundamental rights violation at national scale, potentially undermining trust in government digital services.

**Existing Controls**: Architecture Principle P7 (Privacy by Design and Data Minimisation) is NON-NEGOTIABLE; granular consent management (FR-003); purpose limitation enforced in data model.

---

## 6. Mitigation Measures

### 6.1 Technical Measures

**Data Security**:
- [x] **Encryption at rest** — AES-256 encryption for all personal data in TimescaleDB and object storage (NFR-SEC-003)
- [x] **Encryption in transit** — TLS 1.2+ (preferring TLS 1.3) for all API communications; certificate pinning for mobile app (NFR-SEC-003)
- [x] **Pseudonymisation** — Internal consumer_id (UUID) decoupled from MPAN/MPRN; meter identifiers stored separately from consumption readings with referential integrity
- [ ] **Anonymisation** — Planned for cold-tier consumption data (5+ years) and research purpose aggregation
- [x] **Access controls** — RBAC with least privilege; MFA for all administrative access; GOV.UK One Login for consumer authentication (NFR-SEC-001, NFR-SEC-002)
- [x] **Audit logging** — Comprehensive audit trail with hash chain integrity for all data access, consent changes, and administrative actions (NFR-C-004)
- [ ] **Data masking** — Planned for non-production environments
- [x] **Secure deletion** — Cryptographic erasure for account deletion; automated retention lifecycle enforcement

**Data Minimization**:
- [x] **Collection limitation** — Only 108 attributes across 12 entities; no address, financial, or demographic data beyond minimum identifiers
- [x] **Storage limitation** — Hot/warm/cold tiered retention with automated lifecycle management
- [x] **Processing limitation** — Purpose-bound processing enforced through consent management; each processing activity linked to specific consent purpose
- [x] **Disclosure limitation** — No third-party data sharing; data processors bound by DPAs

**Privacy-Enhancing Technologies**:
- [ ] **Differential privacy** — Planned for aggregated research outputs to prevent re-identification
- [ ] **K-anonymity** — Planned for any publicly released statistical data (minimum k=5)

### 6.2 Organisational Measures

**Policies and Procedures**:
- [ ] **Privacy Policy** — To be developed during Alpha; plain English; WCAG 2.2 AA accessible; available in-app and on web
- [ ] **Data Protection Policy** — Internal DESNZ policy for all staff and contractors with data access
- [ ] **Retention and Disposal Policy** — Automated enforcement with manual review capability; aligned to data model retention periods
- [ ] **Data Breach Response Plan** — 72-hour ICO notification; risk-assessed data subject notification; aligned to NCSC incident management (identified as gap in ARC-001-SECD-v1.0)
- [ ] **Data Subject Rights Procedures** — SAR, rectification, erasure, portability, restriction, objection processes documented and tested

**Training and Awareness**:
- [ ] **Staff training** — UK GDPR awareness for all project team members
- [ ] **Role-specific training** — Enhanced training for database administrators, support staff, and anyone with direct data access
- [ ] **Regular refresher training** — Annual GDPR refresher; ad-hoc training for regulatory changes

**Vendor Management**:
- [ ] **Data Processing Agreements (DPAs)** — Required with DCC, energy supplier API providers, cloud hosting provider, push notification services
- [ ] **Vendor due diligence** — Security and privacy assessment before engagement (aligned to vendor evaluation framework ARC-001-EVAL)
- [ ] **Regular audits** — Annual audits of processor compliance with DPA terms
- [ ] **Data transfer safeguards** — All processors must process data within UK; no international transfers

**Governance**:
- [ ] **Data Protection Officer (DPO)** — CRITICAL: Must be appointed before processing commences (identified as gap)
- [x] **Privacy by Design** — Architecture Principle P7 embedded as NON-NEGOTIABLE from project inception
- [x] **Privacy by Default** — Optional processing purposes (recommendations, tariff comparison, research) are OFF by default; user must affirmatively opt in
- [x] **Regular reviews** — DPIA reviewed quarterly and on any significant processing change

**Data Subject Rights Facilitation**:
- [x] **Subject Access Request (SAR) process** — Automated SAR endpoint (FR-015); response within 1 month
- [x] **Rectification process** — In-app profile editing for consumer data
- [x] **Erasure process** — Account deletion (UC-8) with full data erasure within 30 days; cascade deletion across all entities except legal obligation records
- [x] **Portability process** — JSON and CSV export of consumption data (FR-010)
- [x] **Objection process** — Per-purpose consent withdrawal via in-app management (UC-7)
- [x] **Restriction process** — Purpose-level processing restriction through consent management

### 6.3 Mitigation Mapping

**Risk-by-Risk Mitigation**:

| Risk ID | Risk Title | Mitigations Applied | Responsibility | Implementation Date |
|---------|------------|---------------------|----------------|---------------------|
| DPIA-001 | Unauthorised access | AES-256 encryption, MFA, RBAC, audit logging, certificate pinning, penetration testing | Security Lead | Pre-Beta |
| DPIA-002 | Data breach | Encryption at rest/transit, DLP controls, breach response plan, 72-hour notification, staff training | DPO + Security Lead | Pre-Beta |
| DPIA-003 | Inaccurate data | DCC data quality validation, anomaly detection, user correction mechanism, data quality SLAs with suppliers | Data Steward | Pre-Beta |
| DPIA-004 | Lifestyle inference | Pseudonymisation, access controls, purpose limitation, no third-party profiling, consumption data separated from identity | Enterprise Architect | Pre-Alpha |
| DPIA-005 | Excessive retention | Automated retention lifecycle, tiered storage, regular retention audits, cold-tier anonymisation | Data Governance Lead | Pre-Beta |
| DPIA-006 | Consent failures | Plain English consent, WCAG 2.2 AA, usability testing with vulnerable users, consent version control, withdrawal audit trail | UX Lead + DPO | Pre-Alpha |
| DPIA-007 | Vulnerable user impact | WCAG 2.2 AA, simplified consent flows, assistive technology testing, large text/high contrast, telephone support channel | UX Lead + Accessibility Lead | Pre-Beta |
| DPIA-008 | Function creep | Purpose limitation in data model, NON-NEGOTIABLE Principle P7, consent management, legislative safeguards, annual purpose review | DPO + SIRO | Ongoing |
| DPIA-009 | Re-identification | Differential privacy for research outputs, k-anonymity (k≥5), aggregation thresholds, no individual-level research data release | Data Governance Lead | Pre-Live |
| DPIA-010 | Processor misuse | DPAs with all processors, annual audits, UK-only processing, contractual penalties, right to audit | Legal + Procurement | Pre-Beta |

### 6.4 Residual Risk Assessment

**Risks After Mitigation**:

| Risk ID | Risk Title | Mitigations | Residual Likelihood | Residual Severity | Residual Risk Level | Acceptable? | Justification |
|---------|------------|-------------|---------------------|-------------------|---------------------|-------------|---------------|
| DPIA-001 | Unauthorised access | Encryption + MFA + RBAC + Audit + Pen testing | Low | High | **MEDIUM** | YES | Industry best-practice controls; residual risk from sophisticated attacks accepted with monitoring |
| DPIA-002 | Data breach | Encryption + DLP + Breach plan + Training | Low | High | **MEDIUM** | YES | Cannot eliminate entirely; 72-hour notification and rapid response mitigate harm |
| DPIA-003 | Inaccurate data | Validation + Anomaly detection + User correction | Low | Medium | **LOW** | YES | Data quality SLAs with DCC/suppliers; user can verify against physical meter |
| DPIA-004 | Lifestyle inference | Pseudonymisation + Access controls + Purpose limitation | Low | Medium | **LOW** | YES | Inference risk inherent in energy data; mitigated by preventing third-party access |
| DPIA-005 | Excessive retention | Automated lifecycle + Audits | Low | Low | **LOW** | YES | Technical controls enforce retention; regular audits verify compliance |
| DPIA-006 | Consent failures | Plain English + WCAG 2.2 AA + Usability testing | Low | Medium | **LOW** | YES | Extensive testing with vulnerable user personas reduces consent comprehension risk |
| DPIA-007 | Vulnerable user impact | WCAG 2.2 AA + Simplified flows + Telephone support | Low | Medium | **LOW** | YES | Multi-channel support and accessibility compliance; ongoing user research |
| DPIA-008 | Function creep | Purpose limitation + Principle P7 + Consent + Annual review | Low | High | **MEDIUM** | YES | Strong governance controls; annual purpose review by DPO; legislative change monitoring |
| DPIA-009 | Re-identification | Differential privacy + K-anonymity + Aggregation | Low | Medium | **LOW** | YES | No individual-level data released for research; statistical disclosure controls |
| DPIA-010 | Processor misuse | DPAs + Audits + UK-only + Right to audit | Low | Medium | **LOW** | YES | Contractual and technical controls; UK jurisdiction enables enforcement |

**Overall Residual Risk Level**: MEDIUM

**Acceptability Assessment**:
- [x] All residual risks are LOW or MEDIUM → ACCEPTABLE
- DPIA-001, DPIA-002, and DPIA-008 remain at MEDIUM due to the inherent sensitivity of energy data at national scale and the impossibility of eliminating all breach/creep risk
- No residual risks are HIGH or VERY HIGH

---

## 7. ICO Prior Consultation

**ICO Consultation Required**: NO

**Rationale**: All residual risks have been reduced to MEDIUM or LOW through the mitigation measures described in Section 6. No HIGH or VERY HIGH residual risks remain. ICO prior consultation under Article 36 is therefore not triggered.

**Note**: The ICO should be informed of this DPIA as a matter of good practice given the scale of processing (34 million data subjects) and the government-citizen relationship. This is recommended but not legally required.

---

## 8. Sign-Off and Approval

### 8.1 DPIA Approval

| Role | Name | Decision | Date | Signature |
|------|------|----------|------|-----------|
| **Data Protection Officer** | To be appointed | PENDING | PENDING | PENDING |
| **Data Controller** | DESNZ SRO | PENDING | PENDING | PENDING |
| **Senior Responsible Owner** | DESNZ SRO | PENDING | PENDING | PENDING |

### 8.2 Conditions of Approval

**Conditions** (recommended):
1. DPO must be appointed before any personal data processing commences
2. SIRO must be appointed with clear accountability for data protection risk acceptance
3. Data subject consultation must be completed during Alpha phase with vulnerable user representation
4. All DPAs must be signed with data processors (DCC, energy suppliers, cloud provider) before data flows commence
5. Data breach response plan must be documented, tested, and operational before Beta
6. Penetration testing must be completed before any public-facing deployment

**How Conditions Will Be Met**:
- DPO appointment — Responsibility: DESNZ HR — Due: Before Alpha commences
- SIRO appointment — Responsibility: DESNZ SRO — Due: Before Alpha commences
- Data subject consultation — Responsibility: User Research Lead — Due: During Alpha (Q3 2026)
- DPA execution — Responsibility: Legal/Procurement — Due: Before Beta
- Breach response plan — Responsibility: Security Lead — Due: Before Beta
- Penetration testing — Responsibility: Security Lead — Due: Before Beta

### 8.3 Final Decision

**Decision**: PROCEED WITH CONDITIONS

**Rationale**: The processing is necessary and proportionate to deliver significant public benefit (citizen empowerment, energy cost reduction, net zero contribution). All identified risks can be mitigated to MEDIUM or LOW. Strong data subject controls (granular consent, full rights implementation, privacy by default) provide appropriate safeguards. Processing should proceed subject to the conditions in Section 8.2 being met before relevant project phases.

**Effective Date**: Upon DPO and SIRO appointment and DPIA approval sign-off

---

## 9. Integration with Information Security Management

### 9.1 Link to Security Controls

**Security Assessment Reference**: `projects/001-smart-meter-app/ARC-001-SECD-v1.0.md`

**DPIA Mitigations → Security Controls Mapping**:

| DPIA Mitigation | Security Control | NCSC CAF Principle | Implementation Status |
|-----------------|------------------|--------------------|-----------------------|
| Encryption at rest (AES-256) | Data security — encryption of personal data stores | B3: Data Security | Planned (Pre-Beta) |
| Encryption in transit (TLS 1.2+/1.3) | Network security — encrypted communications | B3: Data Security | Planned (Pre-Beta) |
| MFA for authentication | Identity and access management | B1: Service Protection Policies | Planned (GOV.UK One Login) |
| RBAC with least privilege | Access control — role-based authorisation | B2: Identity and Access Control | Planned (Pre-Beta) |
| Audit logging with hash chain | Security monitoring and audit trail | C1: Security Monitoring | Planned (Pre-Beta) |
| Certificate pinning | Mobile app security — prevent MITM attacks | B3: Data Security | Planned (Pre-Beta) |
| Penetration testing | Vulnerability assessment | B4: System Security | Not started |
| Incident response plan | Breach notification and response | D1: Response and Recovery Planning | Not started (CRITICAL gap) |

### 9.2 Link to Risk Register

**Risk Register Reference**: `projects/001-smart-meter-app/ARC-001-RISK-v1.0.md`

**DPIA Risks to Add to Risk Register**:

| DPIA Risk ID | Risk Register ID | Risk Category | Owner | Treatment |
|--------------|------------------|---------------|-------|-----------|
| DPIA-001 | R-002 (existing) | TECHNOLOGY | Security Lead | Treat (mitigate) — existing risk updated with DPIA mitigations |
| DPIA-002 | R-002 (existing) | TECHNOLOGY | Security Lead | Treat (mitigate) — breach scenario captured under R-002 |
| DPIA-007 | NEW | REPUTATIONAL | UX Lead | Treat (mitigate) — new risk for vulnerable user exclusion |
| DPIA-008 | R-010 (existing) | COMPLIANCE | DPO | Treat (mitigate) — function creep as GDPR non-compliance variant |
| DPIA-010 | R-003 (existing) | OPERATIONAL | Procurement | Treat (mitigate) — processor risk captured under supplier dependency |

---

## 10. Review and Monitoring

### 10.1 Review Triggers

**DPIA must be reviewed when**:
- [x] Significant change to processing (new data, new purpose, new systems)
- [x] New technology introduced (e.g., AI/ML for recommendations)
- [x] New risks identified (e.g., new attack vectors, regulatory changes)
- [x] Data breach or security incident occurs
- [x] ICO guidance changes (e.g., updated DPIA guidance or energy sector code of practice)
- [x] Data subjects raise concerns (e.g., through feedback mechanism or complaints)
- [x] Periodic review date reached (quarterly)
- [x] Smart Energy Code (SEC) changes affecting data access
- [x] DCC infrastructure changes affecting data processing

**Periodic Review Frequency**: Every 3 months (quarterly)

### 10.2 Review Schedule

| Review Type | Frequency | Next Review Date | Responsibility |
|-------------|-----------|------------------|----------------|
| **Periodic review** | 3 months | 2026-05-01 | DPO |
| **Post-Alpha review** | After Alpha phase | TBD (est. Q4 2026) | Enterprise Architect + DPO |
| **Post-implementation review** | 3 months after go-live | TBD | Enterprise Architect + DPO |
| **Annual comprehensive review** | Annually | 2027-02-01 | Data Controller (DESNZ SRO) |

### 10.3 Monitoring Activities

**Ongoing Monitoring**:
- [x] Track number of SARs received and response times
- [x] Track data breaches and near-misses
- [x] Monitor audit logs for unauthorised access attempts
- [x] Review data subject complaints about privacy
- [x] Track compliance with retention periods
- [x] Monitor consent grant/withdrawal rates
- [x] Track vulnerable user engagement with privacy controls

**Monitoring Metrics**:

| Metric | Target | Measurement Frequency | Responsibility |
|--------|--------|----------------------|----------------|
| SAR response time | <1 month | Monthly | DPO |
| Data breaches | 0 | Continuous | Security Team |
| Unauthorised access attempts | <10/month | Weekly | Security Team |
| Consent withdrawal rate | <5% per month | Monthly | Product Owner |
| Retention compliance | 100% | Quarterly | Data Governance Lead |
| Vulnerable user feedback | >80% positive | Quarterly | UX Lead |

### 10.4 Change Management

**Change Control Process**:
1. Any change to processing must be assessed for DPIA impact by the DPO
2. If change is significant (new data, new purpose, new risk), DPIA must be updated
3. Updated DPIA must be re-approved by DPO and Data Controller
4. Data subjects must be notified of significant changes via in-app notification and updated privacy notice

**Change Log**:

| Change Date | Change Description | DPIA Impact | Updated Sections | Approved By |
|-------------|-------------------|-------------|------------------|-------------|
| 2026-02-01 | Initial DPIA creation | N/A | All | PENDING |

---

## 11. Traceability to ArcKit Artifacts

### 11.1 Source Artifacts

**This DPIA was generated from**:

| Artifact | Location | Information Extracted |
|----------|----------|----------------------|
| **Architecture Principles** | `projects/000-global/ARC-000-PRIN-v1.0.md` | Principle P5 (Security by Design), P7 (Privacy by Design), P8 (Data Sovereignty) — all NON-NEGOTIABLE |
| **Data Model** | `projects/001-smart-meter-app/ARC-001-DATA-v1.0.md` | 12 entities, 108 attributes, PII inventory, GDPR lawful basis per entity, retention periods, data volumes |
| **Requirements** | `projects/001-smart-meter-app/ARC-001-REQ-v1.0.md` | Processing purposes (BR/FR/DR), security requirements (NFR-SEC), compliance requirements (NFR-C), data subject rights (FR-003, FR-010, FR-015) |
| **Stakeholder Analysis** | `projects/001-smart-meter-app/ARC-001-STKE-v1.0.md` | 34 million data subjects, vulnerable groups (Margaret, Aisha personas), RACI for data governance roles |
| **Risk Register** | `projects/001-smart-meter-app/ARC-001-RISK-v1.0.md` | R-002 (data breach, residual 15), R-010 (GDPR non-compliance, residual 12) |
| **Secure by Design Assessment** | `projects/001-smart-meter-app/ARC-001-SECD-v1.0.md` | Security controls for DPIA mitigations; DPIA identified as CRITICAL gap (B3, 3.2); SIRO/DPO gaps |

### 11.2 Traceability Matrix: Data → Requirements → DPIA

| Data Model Entity | PII Level | DR Requirement | Processing Purpose | DPIA Risk(s) | Lawful Basis |
|-------------------|-----------|----------------|-------------------|-------------|--------------|
| E-001: Consumer Profile | HIGH | DR-001 | Account management, authentication | DPIA-001, DPIA-002 | Contract (Art 6(1)(b)) |
| E-002: Linked Meter | HIGH | DR-001 | Meter identification for data retrieval | DPIA-001, DPIA-002 | Contract (Art 6(1)(b)) |
| E-004: Consumption Reading | MEDIUM (indirect) | DR-001, DR-002 | Consumption visualisation, recommendations, tariff comparison | DPIA-001, DPIA-003, DPIA-004 | Consent (Art 6(1)(a)) |
| E-007: Recommendation | LOW | DR-002 | Personalised energy-saving advice | DPIA-003, DPIA-006 | Consent (Art 6(1)(a)) |
| E-008: Tariff Comparison | LOW | DR-002 | Informed tariff switching | DPIA-003, DPIA-006 | Consent (Art 6(1)(a)) |
| E-010: Consent Record | MEDIUM | DR-004 | Accountability and audit trail | DPIA-006 | Legal obligation (Art 6(1)(c)) |
| E-012: Audit Log | MEDIUM | NFR-C-004 | Regulatory compliance and security monitoring | DPIA-001 | Legal obligation (Art 6(1)(c)) |

### 11.3 Traceability Matrix: Stakeholder → Data Subject → Rights

| Stakeholder | Data Subject Type | Volume | Rights Processes Implemented | Vulnerability Safeguards |
|-------------|-------------------|--------|------------------------------|--------------------------|
| Citizens (SD-7) | Smart meter householders | 34 million | SAR (FR-015), Rectification, Erasure (UC-8), Portability (FR-010), Objection/Restriction (UC-7) | WCAG 2.2 AA, multi-channel support |
| Citizens — Margaret persona | Elderly/digitally cautious | 5-8 million | All above + simplified consent flows | Large text, simplified UI, telephone support, pre-populated defaults |
| Citizens — Aisha persona | Disabled users | 2-3 million | All above + assistive technology support | VoiceOver/TalkBack, high contrast, semantic HTML |
| Citizens — prepayment users | Fuel-poor households | 4 million | All above | Budget alerts, accessible tariff comparison, no discrimination in recommendations |

### 11.4 Downstream Artifacts Informed by DPIA

**This DPIA informs**:

| Artifact | How DPIA Informs It |
|----------|---------------------|
| **Risk Register** (ARC-001-RISK) | DPIA-007 (vulnerable user impact) added as new risk; DPIA mitigations update R-002 and R-010 controls |
| **Secure by Design Assessment** (ARC-001-SECD) | DPIA mitigations become security control requirements; DPIA completion resolves CRITICAL B3 gap |
| **Vendor HLD Review** | Vendor design must implement DPIA mitigations (encryption, access controls, consent management) |
| **Vendor DLD Review** | Detailed technical controls must match DPIA mitigation requirements |
| **Service Assessment (GDS)** | DPIA demonstrates Point 5 (Make sure everyone can use the service) and data protection compliance |
| **Procurement (SOW)** | DPIA requirements flow into vendor RFP; DPA requirements for all processors |
| **Backlog** | DPIA conditions (DPO appointment, breach response plan, pen testing) generate backlog items |

---

## 12. Data Subject Rights Implementation

### 12.1 Rights Checklist

**Right of Access (Article 15)**:
- [x] Process implemented: Automated SAR endpoint (FR-015) providing structured data export
- [x] Response time: Within 1 month (extendable by 2 months if complex)
- [x] Identity verification: GOV.UK One Login authentication; additional verification for telephone/email requests
- [x] Information provided: Copy of all personal data, processing purposes, categories, recipients, retention periods, rights information
- [x] Free of charge (unless excessive/unfounded)

**Right to Rectification (Article 16)**:
- [x] Process implemented: In-app profile editing for consumer data (E-001); meter data corrections via supplier escalation
- [x] Verification: Cross-reference with DCC/supplier records for meter data accuracy
- [x] Notification: Data processors notified of rectifications

**Right to Erasure (Article 17)**:
- [x] Process implemented: Account deletion (UC-8) with cascade deletion across all entities within 30 days
- [x] Exceptions: Consent records (E-010) and audit logs (E-012) retained for 7 years under legal obligation (Article 6(1)(c))
- [x] Third parties notified: All processors instructed to delete corresponding data

**Right to Restriction of Processing (Article 18)**:
- [x] Process implemented: Per-purpose consent withdrawal restricts processing for that purpose
- [x] Technical implementation: Consent status flag per purpose; processing services check consent before accessing data

**Right to Data Portability (Article 20)**:
- [x] Applicable: YES — automated processing on consent basis
- [x] Process implemented: Data export in JSON and CSV formats (FR-010)
- [x] Format: Machine-readable (JSON, CSV)
- [x] Direct transmission: Planned for future — API-based transfer to another controller

**Right to Object (Article 21)**:
- [x] Process implemented: Per-purpose objection via consent management (UC-7)
- [x] Basis: Applicable for all consent-based processing (objection = consent withdrawal)
- [x] Marketing opt-out: No direct marketing; push notifications are opt-in with granular control

**Rights Related to Automated Decision-Making (Article 22)**:
- [x] Applicable: NO — no solely automated decision-making with legal or similarly significant effect
- [x] Safeguards: Recommendations are advisory only; human decision-making retained for all consequential actions (tariff switching, budget setting)

### 12.2 Rights Fulfillment Procedures

**Standard Operating Procedures**:
1. **Receipt**: Rights requests received via in-app SAR endpoint (primary), email, or telephone support
2. **Verification**: Identity verified through GOV.UK One Login session; additional verification for non-authenticated channels
3. **Logging**: Request logged in audit system (E-012) with unique reference number
4. **Acknowledgement**: Acknowledgement sent within 5 working days
5. **Retrieval**: Data retrieved from TimescaleDB and associated stores
6. **Review**: DPO review for complex requests, exemptions, or third-party data
7. **Response**: Response provided within 1 calendar month
8. **Escalation**: Complex requests escalated to DPO; complaints escalated to ICO

**Training**: All support staff trained on data subject rights procedures; refresher training annually.

---

## 13. International Data Transfers

**Applicable**: NO

All personal data is processed and stored exclusively within UK data centres (AWS eu-west-2 London or Azure UK South). This is mandated by Architecture Principle P8 (Data Sovereignty and Residency), which is classified as NON-NEGOTIABLE.

No personal data is transferred to any country outside the United Kingdom. All data processors (DCC, energy supplier APIs, cloud hosting) process data within UK jurisdiction.

Push notification services (APNS/FCM) transmit notification payloads that do not contain personal data — only generic alert text and a reference identifier.

---

## 14. Children's Data

**Processing Children's Data**: NO

The service is designed for energy bill payers who are named account holders or authorised representatives for smart meter installations. Registration requires linking to a smart meter account, which is held by adults. The service does not knowingly collect or process children's data.

If a child (under 18) were to access the app through a parent's account, this would be covered by the parent's consent and account management. No child-specific profiling, marketing, or processing takes place.

---

## 15. Algorithmic/AI Processing

**Algorithmic Processing**: YES (limited — rule-based only)

### 15.1 Algorithm Description

**Algorithm Type**:
- [x] Rule-based system — Consumption pattern matching for energy-saving recommendations; tariff cost calculation for comparison

**Processing Type**:
- [x] Recommendation — Energy-saving tips based on consumption patterns
- [x] Classification — Consumption pattern categorisation (peak/off-peak, seasonal, appliance inference)

**Human Oversight**:
- [x] Human-on-the-loop — Recommendations are curated by energy experts; algorithm parameters reviewed quarterly; users make all decisions

### 15.2 Algorithmic Bias Assessment

**Protected Characteristics Considered**:
- [x] Age — Elderly users may have different consumption patterns (heating needs); recommendations should not disadvantage
- [x] Disability — Users with medical equipment (oxygen concentrators, electric wheelchairs) should not receive inappropriate reduction recommendations
- [x] Race — No direct relevance to rule-based energy recommendations
- [x] Sex — No direct relevance

**Bias Testing**:
- [ ] Rule-based recommendations reviewed for appropriateness across user demographics — Planned for Alpha
- [ ] Tariff comparison tested to ensure no systematic bias against prepayment meter users — Planned for Alpha

**Bias Mitigation**:
- [x] Recommendations flagged as advisory only
- [ ] User feedback mechanism for inappropriate recommendations — Planned
- [x] No recommendations that could cause harm (e.g., "reduce heating" during cold weather for vulnerable users)
- [ ] Medical equipment usage patterns excluded from reduction recommendations — Planned

### 15.3 Explainability and Transparency

**Explainability Level**:
- [x] Full explainability — Rule-based system with visible decision logic

**Explanation Mechanism**: Each recommendation includes a plain-English explanation of why it was generated (e.g., "Based on your usage between 4-7pm, you could save £X by shifting to off-peak hours"). Tariff comparisons show full calculation methodology.

**ATRS Compliance**: Not required — rule-based system below ATRS threshold. If AI/ML is introduced in future, ATRS record will be required (use `/arckit.atrs`).

---

## 16. Summary and Conclusion

### 16.1 Key Findings

**Processing Summary**:
- Processing 12 categories of personal data across 108 attributes
- Processing 0 special category data types (energy data is behaviourally sensitive but not Article 9)
- Affecting up to 34 million data subjects (UK smart meter households)
- For purposes: Energy consumption monitoring, personalised recommendations, tariff comparison, budget management
- Using lawful bases: Consent (Article 6(1)(a)) for energy data processing; Contract (Article 6(1)(b)) for account management; Legal Obligation (Article 6(1)(c)) for accountability records
- No special category basis required

**Risk Summary**:
- 10 risks identified to data subjects' rights and freedoms
- 4 HIGH risks before mitigation (DPIA-001, DPIA-002, DPIA-007, DPIA-008)
- 3 MEDIUM risks after mitigation (DPIA-001, DPIA-002, DPIA-008)
- 7 LOW risks after mitigation
- 0 HIGH or VERY HIGH risks after mitigation
- Overall residual risk: MEDIUM

**Compliance Summary**:
- [x] Necessity and proportionality demonstrated (Section 4)
- [x] Lawful bases identified per processing purpose (Section 4.1)
- [ ] Data subjects consulted — PLANNED for Alpha phase
- [ ] DPO consulted — PENDING (DPO appointment required)
- [x] Risks identified and mitigated (Sections 5 and 6)
- [x] Data subject rights processes designed (Section 12)
- [x] Security measures specified (Section 6.1, linked to ARC-001-SECD-v1.0)
- [x] Review schedule established (Section 10)

### 16.2 Recommendations

**Recommendations**:
1. **Appoint DPO and SIRO before Alpha** — Critical governance gap; no personal data processing should commence without DPO oversight and SIRO risk acceptance
2. **Complete data subject consultation during Alpha** — Include vulnerable user representatives (elderly, disabled, prepayment meter users) in privacy-focused user research
3. **Implement data breach response plan before Beta** — Document, test, and rehearse breach notification procedures including 72-hour ICO notification
4. **Execute DPAs with all data processors** — DCC, energy supplier API providers, and cloud hosting provider must have signed DPAs before data flows commence
5. **Conduct penetration testing before public deployment** — Validate security controls against OWASP MASVS and NCSC mobile security guidance
6. **Implement differential privacy for research outputs** — Any anonymised/aggregated data released for policy research must use statistical disclosure controls

**Actions Required Before Go-Live**:

| Action | Responsibility | Due Date | Status |
|--------|----------------|----------|--------|
| Appoint DPO | DESNZ HR | Before Alpha | Not Started |
| Appoint SIRO | DESNZ SRO | Before Alpha | Not Started |
| Data subject consultation (vulnerable users) | User Research Lead | During Alpha | Not Started |
| Sign DPAs with DCC, suppliers, cloud provider | Legal/Procurement | Before Beta | Not Started |
| Document and test breach response plan | Security Lead + DPO | Before Beta | Not Started |
| Penetration testing | Security Lead | Before Beta | Not Started |
| Privacy notice development and testing | DPO + UX Lead | Before Beta | Not Started |
| DPIA review and DPO sign-off | DPO | Before Beta | Not Started |
| DPIA approval by Data Controller | DESNZ SRO | Before Beta | Not Started |

### 16.3 Final Conclusion

**Conclusion**: PROCEED WITH CONDITIONS

**Rationale**: This DPIA demonstrates that the UK Smart Meter Data Consumer Mobile App processes personal data in a manner that is necessary, proportionate, and capable of being adequately safeguarded. The processing delivers significant public benefit — empowering 34 million households to understand and reduce their energy consumption, supporting UK net zero targets, and promoting energy market competition. All 10 identified risks to data subjects can be reduced to MEDIUM or LOW through specified technical and organisational measures. ICO prior consultation is not required. Processing should proceed subject to the conditions listed in Section 8.2.

**Conditions**:
- DPO and SIRO must be appointed before any personal data processing
- DPAs must be executed with all data processors before data flows commence
- Data subject consultation with vulnerable user representatives must be completed during Alpha
- Data breach response plan must be operational before Beta
- Penetration testing must be completed before public deployment
- This DPIA must be reviewed and approved by the DPO before processing commences

**Sign-Off**: This DPIA has been completed. Approval is PENDING DPO appointment and review.

---

## Generation Metadata

**Generated by**: ArcKit `/arckit.dpia` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.0.4
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**Model**: Claude Opus 4.5

**Traceability**: This DPIA is traceable to architecture principles (ARC-000-PRIN-v1.0), data model (ARC-001-DATA-v1.0), requirements (ARC-001-REQ-v1.0), stakeholders (ARC-001-STKE-v1.0), risk register (ARC-001-RISK-v1.0), and secure by design assessment (ARC-001-SECD-v1.0) via the ArcKit governance framework.

---

## Appendix A: ICO DPIA Screening Checklist

Full screening questionnaire (9 criteria) with detailed YES/NO responses:

1. ☑ **Evaluation or scoring** — YES: Personalised recommendations evaluate consumption patterns; tariff comparison scores suitability
2. ☐ **Automated decision-making with legal/significant effect** — NO: All recommendations are advisory; no automated decisions with legal effect
3. ☑ **Systematic monitoring** — YES: Continuous half-hourly consumption monitoring via DCC infrastructure
4. ☐ **Sensitive data or highly personal data** — NO: No Article 9 special category data (energy data is behaviourally sensitive but not Article 9)
5. ☑ **Large scale processing** — YES: 34 million data subjects, 150 billion records, UK-wide geographic scope
6. ☐ **Matching or combining datasets** — NO: Dataset combination is reasonably expected by users of an energy monitoring app
7. ☑ **Vulnerable data subjects** — YES: Elderly, disabled, and prepayment meter users (financially vulnerable)
8. ☐ **Innovative technology** — NO: Standard mobile app, established database, standard APIs
9. ☐ **Processing prevents exercising rights** — NO: Full data subject rights implemented

**Result: 4/9 criteria met → DPIA REQUIRED**

---

## Appendix B: GDPR Article 35 Requirements Checklist

| Article 35 Requirement | Addressed in Section | Complete? |
|------------------------|---------------------|-----------|
| Systematic description of processing | Section 2 | ✓ |
| Purposes of processing | Section 2.3, 2.4 | ✓ |
| Assessment of necessity and proportionality | Section 4 | ✓ |
| Assessment of risks to data subjects | Section 5 | ✓ |
| Measures to address risks | Section 6 | ✓ |
| Safeguards, security measures | Section 6.1, 9.1 | ✓ |
| Demonstrate compliance with GDPR | Throughout | ✓ |

---

## Appendix C: Data Protection Principles Compliance

**GDPR Article 5 Principles**:

| Principle | Assessment | Evidence |
|-----------|------------|----------|
| **(a) Lawfulness, fairness, transparency** | COMPLIANT | Lawful bases identified per purpose (Section 4.1); privacy notice planned; granular consent management |
| **(b) Purpose limitation** | COMPLIANT | Purposes clearly defined (Section 2.3); purpose limitation enforced through consent management and Architecture Principle P7 |
| **(c) Data minimisation** | COMPLIANT | 108 attributes justified per entity; no excessive collection; no address/financial/demographic data beyond minimum |
| **(d) Accuracy** | COMPLIANT | DCC data quality validation; anomaly detection; user rectification mechanism (Section 12.1) |
| **(e) Storage limitation** | COMPLIANT | Tiered retention (90 days/2 years/5 years/7 years); automated lifecycle management (Section 2.2) |
| **(f) Integrity and confidentiality** | COMPLIANT | AES-256 encryption, TLS 1.2+, MFA, RBAC, audit logging, certificate pinning (Section 6.1) |
| **Accountability** | PARTIAL | DPIA completed; architecture principles embedded; DPO appointment PENDING; SIRO appointment PENDING |

---

## Appendix D: Glossary

| Term | Definition |
|------|------------|
| **Data Subject** | An identified or identifiable natural person whose personal data is being processed |
| **Data Controller** | The organisation that determines the purposes and means of processing personal data (DESNZ for this service) |
| **Data Processor** | An organisation that processes personal data on behalf of the controller (e.g., DCC, cloud hosting provider) |
| **Personal Data** | Any information relating to an identified or identifiable natural person |
| **Special Category Data** | Sensitive personal data (race, health, biometric, etc.) requiring Article 9 basis |
| **Processing** | Any operation performed on personal data (collection, storage, use, disclosure, deletion) |
| **Profiling** | Automated processing to evaluate personal aspects (predict performance, behaviour, preferences) |
| **Pseudonymisation** | Processing that prevents identification without additional information kept separately |
| **Anonymisation** | Irreversibly removing identifying information so re-identification is not possible |
| **Lawful Basis** | Legal ground for processing under GDPR Article 6 (consent, contract, legal obligation, etc.) |
| **DPIA** | Data Protection Impact Assessment — required for high-risk processing under Article 35 |
| **ICO** | Information Commissioner's Office — UK data protection supervisory authority |
| **UK GDPR** | UK General Data Protection Regulation (retained EU GDPR post-Brexit) |
| **DPA 2018** | Data Protection Act 2018 — UK law supplementing UK GDPR |
| **DCC** | Data Communications Company — smart meter infrastructure operator |
| **SMETS** | Smart Metering Equipment Technical Specifications (SMETS1/SMETS2) |
| **MPAN** | Meter Point Administration Number — unique electricity meter identifier |
| **MPRN** | Meter Point Reference Number — unique gas meter identifier |
| **SEC** | Smart Energy Code — industry code governing smart metering |
| **DESNZ** | Department for Energy Security and Net Zero |
| **SIRO** | Senior Information Risk Owner |
| **DPO** | Data Protection Officer |
| **SAR** | Subject Access Request |
| **DPA (agreement)** | Data Processing Agreement — contract between controller and processor |
| **SCC** | Standard Contractual Clauses — mechanism for international data transfers |

---

**END OF DPIA**

---

**Generated by**: ArcKit `/arckit.dpia` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.0.4
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**Model**: Claude Opus 4.5
