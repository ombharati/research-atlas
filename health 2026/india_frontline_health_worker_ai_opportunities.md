# AI Assistance Opportunities for India's Frontline Rural Health Workforce
## A deep-dive investigation of ASHA, ANM, and Anganwadi worker workflows, pain points, and realistic AI leverage points

**Compiled: October 2026**
**Sources: peer-reviewed time-motion and qualitative studies, government documents (MoHFW/PIB/NHRC), platform evaluations (TeCHO+, ANMOL, Poshan Tracker, U-WIN, Ni-kshay), NGO and journalism field reports (BehanBox, New Lines, CodaStory, Livemint, TOI), CHI/ACM research (ASHABot), and current AI deployments (HealthVaani, SMARThealth GPT).**

---

## 1. Executive Summary

India's rural primary health system runs on an informal, overwhelmingly female workforce: ~1.05 million ASHAs (Accredited Social Health Activists), ~219,000 ANMs (Auxiliary Nurse Midwives), and ~1.3 million Anganwadi workers and helpers (AWWs), plus male health workers, ASHA facilitators, and Community Health Officers at ~1.7 lakh Ayushman Arogya Mandirs [R1][R2][R3].

Time-motion studies and field reporting converge on one finding: **a large and growing share of these workers' time is consumed not by care, but by data work** — maintaining parallel paper registers and multiple siloed government apps, chasing due lists, assembling monthly reports, obtaining signatures, verifying beneficiary payments, and reconciling records across systems. Specific quantified evidence:

- ASHAs in central India average ~4.3 hours/day of programme work spread across 7 days a week; national-programme activities, register maintenance, training/meetings, and surveys together consume more time than home visits [R4].
- ANMs spend a median of 7 hours 4 minutes per working day; AWWs 6 hours 50 minutes [R5].
- AWWs in Madhya Pradesh spend an average of 51 minutes/day on paper registers (vs. 30 minutes "expected"); 83% exceed the expected time; each maintains ~11 registers for ~1,000 beneficiaries — while also being required to keep paper records as a "failsafe" alongside the Poshan Tracker app [R6].
- Some states require up to **38 registers at the sub-centre level** (ANM) [R7].
- One ASHA in Maharashtra needs **~2 days to enter 200 TB patients into Ni-kshay**, with frequent error messages forcing re-entry; another juggles **seven apps plus WhatsApp groups, Google Sheets and Excel files** demanded by supervisors; the ABHA health-ID app **logs out every 15 minutes with no save option** [R8].
- TeCHO+ (Gujarat) — the one platform with genuine workflow automation (work-plan generation + risk alerts) — saved ANMs **1.7 hours/day** and data-entry operators 1.5 hours/day, and improved data concordance from 69% to 81% [R9]. This is the strongest available proof that digitizing workflow (not just digitizing forms) pays off.

Meanwhile, the knowledge gap that training was supposed to close persists: a 2025 systematic review of 37 studies pooled ASHA knowledge at ~62% (maternal health) and ~69% (neonatal/child health), with specific weaknesses in danger-sign recognition and referral decisions; two-thirds of ASHAs in one Assam study had not received the full 23 days of recommended training [R10][R11].

**Existing digital platforms do not solve these problems because they were built as monitoring instruments for the state, not as work aids for the worker**: they fragment data across silos, duplicate rather than eliminate paper work, assume literacy/English/connectivity that many workers lack, give dashboards to officers but nothing actionable back to the worker, embed surveillance (GPS, photo/facial-recognition attendance), and provide almost no decision support, drafting, synthesis, or local-language interaction [R6][R8][R12][R13][R14][R15].

The 2023–2026 wave of LLM-based pilots — **ASHABot** (Microsoft Research/Khushi Baby, WhatsApp-based, Hindi + voice, CHI 2025) [R16], **HealthVaani** (Wadhwani AI/Gates Foundation, embedded in Poshan Tracker, 6 states) [R17], and **SMARThealth GPT** (George Institute/Oxford, inside the SMARThealth Pregnancy tablet app, Hindi/Telugu) [R18] — demonstrates that voice-first, local-language, protocol-grounded AI assistants are already feasible, trusted, and used by this workforce, and that the ORF-proposed "AI Sahayak" national architecture (open protocol, error audits, worker liability protection, kill-switches) is under active policy discussion as of mid-2026 [R19].

This report maps **19 concrete opportunity areas** across six task families (documentation & data entry, due-lists & planning, reports & incentives, decision support, communication & coordination, logistics & supervision). For each, it specifies what the worker has, what she lacks, what decisions she makes, which tools she uses today, why those tools fall short, what an AI assistant could realistically do **without replacing her**, and what guardrails are required.

---

## 2. Method and Evidence Base

This investigation synthesizes four evidence streams:

1. **Peer-reviewed field studies** — time-motion studies (Khandre et al. 2022, Wardha [R4]; Singh et al. 2018, Andhra/Telangana [R5]; Jain et al. 2020, MP Anganwadis [R6]), qualitative studies (Gore et al. 2022 JOGH [R20]; ANMOL perception study, AIIMS Raebareli 2026 [R21]; CBAC mixed-methods study, Gujarat 2025 [R22]; ASHA diary usability study, Patel & Tandon 2025 [R23]; workload multi-stakeholder study 2022 [R24]), and platform evaluations (TeCHO+ Gujarat [R9]; ReMiND UP [R25]; Mobile Kunji Bihar [R26]).
2. **Government documents** — PIB ASHA task and incentive schedules [R2]; NHM Joint Review Mission aide-memoires [R7]; NHSRC sub-centre planning and ASHA facilitator handbooks [R27][R28]; WHO India immunization handbook and VHSND guidelines [R29][R30]; National Sickle Cell Anaemia Elimination Mission [R31]; SAHI (Strategy for AI in Healthcare, Feb 2026) [R32].
3. **Journalism and worker voices** — New Lines Magazine (March 2026, "India's Digital Health Push Is Overworking Its Front-Line Women") [R8]; BehanBox (AWW data labour in Tamil Nadu, May 2025 [R12]; Mumbai ASHAs on Census duty, June 2026 [R13]); Livemint (Poshan Tracker protests, 2021) [R14]; CodaStory (Shield 360 GPS surveillance app, Haryana, 2021) [R15]; The Hindu/TOI/New Indian Express protest coverage on delayed honoraria and incentives [R33][R34]; ThePrint on Dalit ASHA labour conditions [R35]; RTH Resources programme review (15 surveys/year in Karnataka) [R10].
4. **AI/digital precedent projects** — ASHABot (CHI 2025) [R16]; HealthVaani [R17]; SMARThealth GPT [R18]; mSakhi [R36]; ORF "Protocol in Every Pocket" (July 2026) [R19]; eSanjeevani scale data [R37].

Where workers' own accounts and quantitative studies disagree, both are reported. State variation is large (Gujarat's TeCHO+ ecosystem vs. Maharashtra's app sprawl vs. Tamil Nadu's dual ICDS apps); opportunities are framed for the modal case with state-specific notes.

---

## 3. The Workforce: Roles, Pay, Supervision, Tools

### 3.1 Who they are

| Cadre | Numbers | Norm (population) | Status & pay | Supervision |
|---|---|---|---|---|
| **ASHA** | ~1.05 million (Sept 2019) [R2] | 1,000 rural population; actual average served ~1,923, >60% serve >1,200 [R24] | "Honorary volunteer"; fixed honorarium (₹2,000/month central norm since 2018; states top up; Mumbai CHVs: ₹1,650 base + ₹4,000–8,500 incentives) + ~30–60 task-linked incentives [R2][R13] | ANM at sub-centre; ASHA facilitator (1 per 10–20 ASHAs, ~20 supervisory visits/month) where it exists [R28][R38] |
| **ANM (MPW-F)** | ~219,000 (2018) [R3] | Sub-centre of 3,000–5,000 | Government employee (18 months' training); salaried | Health Assistant/MPW-M; PHC Medical Officer |
| **AWW** | ~1.3 million incl. helpers (2018) [R3]; ~10.5 lakh AWWs + ~9 lakh helpers | Anganwadi centre of ~1,000 (700 hilly/tribal) | Honorary but with monthly honorarium; ICDS/WCD department (not Health) | CDPO (Child Development Project Officer); Mukhya Sevika |
| **Male MPHW / Health Assistant** | ~90,000+ at sub-centre/PHC level [R5] | Sector of ~5 sub-centres | Salaried | PHC MO |
| **CHO** (Ayushman Arogya Mandir) | ~50,000+ sanctioned at HWCs | 5,000 population | Contractual, mid-level provider | Medical Officer, tele-consult support via eSanjeevani |
| **ASHA facilitator** | State-dependent (Kerala, Assam, Rajasthan, etc.) | 10–20 ASHAs | Incentive-based (₹6,000/month norm) [R38] | MPW/ANM |

Key structural facts that shape every AI opportunity:
- **Two departments, one village**: ASHA/ANM report to Health (NHM); AWW reports to Women & Child Development (ICDS). "Convergence" is mandated (VHSND days, joint registers) but data systems (RCH/U-WIN/Ni-kshay/NCD portal vs. Poshan Tracker) are owned by different ministries and rarely interoperate [R6][R12].
- **Pay is entangled with data**: ASHA incentives are released only after verification chains (beneficiary confirmation → ANM/facilitator sign → block-level compilation → DBT); AWW honorarium was formally linked to Poshan Tracker data entry [R14][R39]. Data work is literally how workers get paid, so data tools are experienced as instruments of payment control.
- **Devices and connectivity**: most workers use **personal** smartphones of modest spec; government-issued devices (e.g., 2GB Panasonic handsets for Poshan Tracker) often can't run the apps; rural coverage is patchy, and workers climb terraces or travel kilometres for signal; a 2025 government survey found ~64% of rural women cannot perform basic smartphone tasks [R8][R14].
- **Language**: interfaces are frequently English-first while workers studied in Marathi/Hindi/Telugu/Tamil mediums; English terminology in forms is a repeatedly reported barrier [R8][R14].
- **Gender norms** restrict phone ownership/use for some women, and night-time data entry happens after household work — the "invisible second shift" [R8].

### 3.2 The current digital stack (2026)

| Platform | Owner | Who uses it | What it does | Known field problems |
|---|---|---|---|---|
| RCH portal / eMamta (Gujarat) & state variants | MoHFW / states | ANM, ASHA, DEO | MCH tracking, due lists, incentive workflows | Data entry at facility by DEOs; worker-facing features thin; state fragmentation [R40] |
| **ANMOL** (Mobile Health for ANMs) | MoHFW (Gujarat origin, multi-state) | ANM | Due lists, tracking of EC/PW/children, immunization | Internet dependence, glitches, duplicate entry; >50% ANMs report training need; workers request ASHA-wise views [R21][R41] |
| **TeCHO+** (Gujarat) | Govt. Gujarat | ANM, ASHA, DEO, MO | Real-time entry, **auto-generated work plans**, high-risk decision-support alerts, dashboards | Gujarat-only; the benchmark of what workflow automation can achieve (1.7 h/day ANM saving) [R9] |
| **U-WIN** | MoHFW (national UIP) | ANM, ASHA, MO | Digitized immunization registry, due lists, digital vaccine cards | Teething issues; low early adoption; duplicate entry vs. paper tally sheets until fully transitioned; state EMRs (TN PICME) being API-linked specifically to cut re-entry [R42][R43] |
| **Ni-kshay** (TB) | NTE/CTD | TB staff, ASHA/TS, facility | Case notification, adherence, DBT (Ni-kshay Poshan), DATS | Extremely heavy manual entry (2 days/200 patients reported), error messages, transfers between systems [R8][R44] |
| **NCD portal / NPCDCS** | MoHFW | ANM, MO, ASHA (CBAC data) | CBAC screening records, HT/DM follow-up | Portal issues reported; CBAC is paper-first in most states; screening→referral cascade leaks (23% attended PHC after high-risk CBAC) [R22] |
| **Poshan Tracker** | WCD | AWW, helper, supervisors | Attendance (geofenced; group-photo; facial recognition for THR), growth monitoring, THR, SNP/PSE records, dashboards | Mandated with pay-cut threat; device inadequacy; English entry; geofence failures forcing daily reinstalls; duplicate paper registers still required; **workers cannot see their own data**; surveillance backlash [R6][R12][R14] |
| **ABDM (ABHA app, health IDs, records)** | NHA | ASHA/CHO for enrolment; facilities | ABHA ID creation, record linking | 15-min session timeout with no save; complex forms; low rural uptake/digital literacy [R8][R45] |
| **eSanjeevani** | MoHFW | CHO/ANM at AAMs; patients | Teleconsultation (481M+ consults; 140k+ AAMs) [R37] | Works well at scale but is a doctor-facing service; the ASHA's coordination labour around it (mobilizing patients, follow-up, medicine pickup) is unsupported |
| Census/SIR apps (2026–27) | Registrar General / ECI | ASHA enumerators | Digital household enumeration (33-question form) | Overheating phones, glitches, heat-hour fieldwork, unpaid delays; work collides with health duties [R13][R34] |
| State attendance/surveillance apps (e.g., Shield 360 Haryana 2021; photo-attendance in Chh. Sambhajinagar 2025) | States | ASHA | GPS tracking, remote device management | Worker protests; privacy violations; trust damage [R15][R46] |

**The pattern**: every programme added a silo; none removed paper; almost none give decision support or save drafting/synthesis time; the worker-facing return on data entry is close to zero. WhatsApp groups + Excel/Google Sheets have become the *de facto* integration layer — informal, unrecorded, unpaid [R8].

---

## 4. Daily Workflow Maps (What Workers Actually Do)

### 4.1 ASHA — a composite day/week/month

**Daily (field days):**
1. Morning: collect day's instructions at health post/sub-centre (in some cities attendance is marked 10am–12pm) [R13]; check WhatsApp groups for circulars, targets, camp notices.
2. House visits: ANC registration and motivation (4 ANC visits), PNC/HBNC home visits on fixed days (3, 7, 14, 21, 28, 42 for institutional births; +day 1 for home births), HBYC child visits (months 3, 6, 9, 12, 15), TB patient home visits/adherence support, NCD patient follow-up, IFA/ORS/albendazole distribution from drug kit, counselling on breastfeeding/complementary feeding/family planning, ABHA enrolment, welfare-scheme linkage [R2][R47].
3. Escort duties: accompany pregnant women/sick children to PHC/CHC/FRU for delivery or treatment; JSY paperwork support [R2].
4. Record everything in the **ASHA diary/family folders** (often 4+ notebooks: family survey, eligible couples, pregnant women, births/deaths) [R8][R23].
5. Evening "second shift": transfer paper records into apps (RCH/eMamta or state MCH app, U-WIN entries via ANM, Ni-kshay, NCD portal, ABDM), respond to supervisors' WhatsApp demands (photos of activities, Excel returns), chase beneficiaries to confirm whether incentive money arrived (needed for her own verification slips) [R4][R8].

**Weekly/monthly:**
- Prepare **due lists** for immunization sessions and ANC/PNC; mobilize for VHND/VHSND (monthly fixed day) jointly with ANM and AWW [R29][R30].
- Attend **sector meeting** (with ANM/facilitator) and **monthly PHC meeting** (2–3 h: review, training, report submission, incentive verification, collecting signatures — "the job of getting signatures is too troublesome") [R4][R48].
- Submit monthly reports (MCH, programme-specific), incentive claim forms with verification slips; attend trainings (often now via WhatsApp videos/PPT) [R8].
- Growth monitoring support at Anganwadi (weighing day), SAM/MAM referral and follow-up, MAA/IFA campaigns, deworming rounds.

**Periodically (campaigns/surveys):** Census/SIR enumeration (2025–27) [R13][R34]; sickle-cell screening mobilization (target 7 crore) [R31]; CBAC NCD household screening (30+ population) [R22]; NFHS-type surveys; polio rounds; filariasis MDA; election duty as BLOs; Karnataka ASHAs reported **15 different surveys in one year** [R10].

### 4.2 ANM (MPW-F) — sub-centre anchor

**Fixed weekly schedule (IPHS norms):** sub-centre OPD/ANC clinic days (2 days), immunization sessions (2–4 days at session sites with ASHA/AWW), home visits for high-risk cases, VHND/VHSND once a month, school health, sector meeting with ASHAs, monthly PHC meeting/reporting [R27][R29].

**Core recurring tasks:**
1. Maintain registers — eligible couple register (with contraception status), MCH register (ANC/intranatal/PNC), birth & death register, immunization register + tally sheets, drug/stock registers, survey registers. JRM documented **up to 38 registers at sub-centre level in some states** [R7].
2. **Immunization micro-planning**: session-wise due lists, monitoring of left-outs/drop-outs after every session (per WHO India handbook, ANM + ASHA/AWW must review the due list and enter names for follow-up), cold-chain/vaccine indent, AEFI reporting [R29].
3. Conduct/assist deliveries at sub-centre where permitted; ANC check-ups (BP, weight, IFA); refer high-risk; track referrals.
4. Enter data: ANMOL/TeCHO+/eMamta/U-WIN/RCH; verify ASHA incentive claims (signing verification slips); compile monthly/quarterly reports for the PHC.
5. Supervise 8–10 ASHAs: field visits, on-the-job training, reviewing ASHA diaries, monthly meeting.
6. NCD: OPD days for HT/DM at sub-centre/AAM, follow-up registers, eAushadhi-style drug logistics; support CHO at AAM; facilitate eSanjeevani teleconsultations.
7. TB: notification support, treatment supervision oversight.

Time evidence: median 7:04 h/day on job (South India), with MCH prioritized; Meghalaya study similarly shows heavy documentation and outreach load [R5][R49].

### 4.3 Anganwadi Worker (AWW) — centre-based + outreach

**Daily at the centre:** open centre; mark own + children's attendance (Poshan Tracker: geofenced app opening, group photo upload, facial-recognition capture for THR distribution in TN); preschool education (~2 h norm; actual average 95 min); hot cooked meal service (SNP) with quantity/stock recording; take-home ration (THR) distribution with photo/FR evidence; growth monitoring (weight/height, MUAC) on scheduled days — but only ~3% of observed time, and 49% of centres lacked growth charts; fill **~11 paper registers** (survey register, birth/death, attendance, SNP, PSE, THR, growth monitoring, MPR data, meetings…) — average 51 min/day, 83% exceed norms; enter the same data into Poshan Tracker (+ a second state app in TN); report stock indents [R6][R12][R14].

**Monthly:** MPR (Monthly Progress Report) compilation and upload (often from terrace/bus-stand for signal); sector meeting with Mukhya Sevika/CDPO; VHSND participation with ANM/ASHA; Poshan Maah activities with photo evidence; PSE curriculum reporting; SAM/MAM referral and follow-up with ASHA.

**Home visits:** only ~9% of daily time despite ICDS guidelines requiring visits to children/PW/PLW — squeezed out by centre duties and data work [R6].

### 4.4 Others in the ecosystem

- **ASHA facilitator**: 20 supervisory visits/month to 10–20 ASHAs; verify diaries, support incentive claims, on-the-job training, data quality checks; herself incentive-paid with heavy verification paperwork [R28][R38].
- **Male MPHW/Health Assistant**: supervision of sub-centres, epidemic/vect or-borne disease work, school health, logistics; median 5:44 h/day [R5].
- **CHO at AAM**: OPD, NCD screening/diagnosis (with tele-support), eSanjeevani facilitation, drugs; supervises ANM/ASHA at AAM; drowning in portal entries across NCD/TB/MCH systems.
- **TB Treatment Provider/Supervisor, Ni-kshay Mitra coordinators**: DATS boxes, follow-up visits, DBT tracking [R44].
- **VHSNC members/PRI**: village health plans — nominally convened with ASHA support, weakly functioning [R10].

---

## 5. Time Evidence Summary (Quantified Burden)

| Evidence point | Source |
|---|---|
| ASHA average work: 4.29 h/day, 7 days/week; largest components: national programmes 66 min, MCH 42 min, register maintenance 41 min, training/meetings 38 min, surveys 31 min, home visits only 19 min, reporting 5 min | Khandre et al., Wardha (17 ASHAs, 4 months) [R4] |
| ANM median 7:04 h/day; male MPHW 5:44 h; AWW 6:50 h | Singh et al., AP/Telangana [R5] |
| AWW: registers 51 min/day (>expected for 83%); preschool 95 min; home visits 9% of time; growth monitoring 3%; 11 registers/~1,000 beneficiaries; app + paper duplication | Jain et al., MP [R6] |
| Up to 38 registers at sub-centre in some states | NHM JRM-8 [R7] |
| 2 days to enter 200 TB patients in Ni-kshay; 7 apps + WhatsApp/Sheets/Excel; ABHA app 15-min timeout, no save; midnight data entry | New Lines 2026 [R8] |
| TeCHO+ saved ANM 1.7 h/day, DEO 1.5 h/day; data concordance 69.1%→80.5%; coverage gains (full ANC 67.9%→75.6%, HBV0 35.3%→67.2%) | Saha & Quazi 2022 [R9] |
| 15 surveys/year (Karnataka ASHAs); incentive verification "cumbersome"; payment delays 3–4 months | RTH 2024 [R10]; protests [R33][R34] |
| ASHA knowledge: 62% maternal / 69% child health (pooled, 37 studies); weak referral/danger-sign knowledge; 2/3 not fully trained (Assam) | Systematic review 2025 [R10][R11] |
| CBAC: 95% form coverage but only 23% of high-score referrals reached PHC; 21% diagnosed; NCD portal issues | Mehta et al. 2025 [R22] |
| AWW digital load doubled in TN (Poshan + TN ICDS + facial recognition); geofence failures force daily reinstalls; workers cannot access their own data | BehanBox 2025 [R12] |
| eSanjeevani: 481M+ teleconsults via 140k+ AAMs | MeitY 2026 [R37] |

---

## 6. Cross-Cutting Pain Points (Task Families That Consume Time or Introduce Errors)

### P1. Dual/duplicate documentation (paper + app, app + app)
Registers were never retired when apps arrived; in TN, two parallel state/central ICDS apps both demand entry [R12]. ASHAs keep 4 notebooks and re-enter into multiple portals [R8]. Every duplication is a fresh error opportunity (transcription mistakes, date errors, name spelling variance) and a nightly time tax.

### P2. Fragmentation across siloed platforms
The same pregnant woman exists separately in RCH/eMamta, U-WIN (for her child), Ni-kshay (if TB), NCD portal (if 30+), ABDM, and state apps — with no shared identifier resolution at the worker's level. Workers perform "human ETL": copying between apps, WhatsApp, and Excel. Interoperability exists as an aspiration (TN's PICME↔U-WIN API linkage was explicitly prioritized to cut data entry [R43]) but is not the norm.

### P3. Due-list preparation and tracking is manual and error-prone
Immunization left-outs/drop-outs must be identified after every session by manual review of due lists [R29]; ANC/PNC/HBNC/HBYC schedules are date-arithmetic on registers. Missed due lists = missed children and lost incentives. ANMOL/TeCHO+ generate due lists where implemented, but workers report the lists don't reflect ground reality (migrations, name duplicates) and require manual reconciliation with their own diaries [R21][R9].

### P4. Monthly reporting and signature-chasing
Monthly reports (MCH, programme, incentive) are assembled by hand from registers, then physically signed by ANM/MO/CDPO ("collect this paper, that paper and get it signed from sister... the job of getting signatures is too troublesome" — ASHA, Wardha) [R4]. Rejections restart the cycle.

### P5. Incentive verification and payment tracking
ASHA pay depends on ~30–60 task-linked incentives with bundled conditions (e.g., a single lump sum requires completing a whole ANC series), verification slips, beneficiary confirmation (ASHAs must ask women whether money arrived — women often don't volunteer it), ANM signature, block compilation, and DBT. Result: chronic delays (3–4 months' arrears are protest-level grievances [R33][R34]), rejections workers cannot diagnose, and substantial monthly clerical labour [R10][R39]. Incentive design itself (lump-sum, all-or-nothing) is documented as demotivating [R39].

### P6. Decision support vacuum at the point of care
ASHAs make consequential judgement calls — danger signs in pregnancy/newborns, referral triggers, CBAC scores, growth classification, TB side-effects — from memory of training received years ago (often incomplete). Reference material is inadequate for complex queries; ANM is supervising multiple villages and hard to reach; monthly meetings don't allow individual questions; sensitive topics (sexual health, GBV) are hard to ask supervisors [R16][R11]. Knowledge is measurably weakest exactly where risk is highest (referral decisions for severe diarrhoea/ARI, danger signs) [R11].

### P7. Follow-up and referral feedback loops are broken
After referral, ASHAs rarely learn what the hospital diagnosed or advised; high-risk CBAC referrals leak (77% never reached a PHC) [R22]; SAM-discharge follow-up depends on memory. No system closes the loop back to the village.

### P8. Coordination friction between cadres
ASHA–AWW–ANM convergence is mandated but uninstrumented: duplicate visits, data disputes ("AWWs don't know most beneficiary information; we gather everything but they take credit" — ASHA FGD [R4]), VHND planning by word of mouth, no shared task view across the two ministries' systems.

### P9. Usability, language, connectivity, devices
English-first forms, layered menus, 15-minute session timeouts, 2GB-RAM devices, geofence failures requiring daily app reinstalls, terrace-hunting for signal, 35MB apps that won't install on issued phones [R8][R12][R14]. Training migrated to WhatsApp videos/PPTs that older or less-literate workers find unhelpful [R8].

### P10. Surveillance and trust deficit
GPS tracking (Shield 360), photo/facial-recognition attendance, pay-linked data mandates created organized resistance ("Mobile vaapsi andolan") and deep suspicion of any new tool; workers cannot even see the data they generate [R15][R12][R14]. Any AI assistant inherits this trust deficit unless designed against it.

### P11. Unpredictable campaign/survey stacking
Census 2026–27, SIR, sickle-cell screening (7-crore target), CBAC rounds, polio/MDA rounds, elections stack on top of routine work without removing it; surveys are "a double-edged sword" — they bring temporary purpose and income but disrupt continuity of care and are often unpaid/delayed [R4][R10][R13][R31][R34].

### P12. Non-clinical cognitive load
Scheme eligibility navigation (JSY, PMMVY, Nikshay Poshan DBT, Ayushman cards, rations), beneficiary bank-linkage issues (fear of scams; women refusing to share account numbers), rumor/misinformation management, and emotional labour with households — all done from memory and WhatsApp forwards [R4][R8].

---

## 7. Why Existing Digital Platforms Don't Solve These Problems

A synthesis across TeCHO+, ANMOL, Poshan Tracker, U-WIN, Ni-kshay, NCD portal, ABDM apps and state tools:

1. **Built for upward monitoring, not downward support.** Data flows to district/state dashboards; almost nothing actionable flows back to the worker. AWWs in TN literally cannot access the data they upload [R12]. Dashboards measure the worker; they don't help her.
2. **Digitization ≠ automation.** Apps replicate paper forms field-for-field. TeCHO+ is the exception that proves the rule: its value came from *auto-generated work plans* and *decision-support alerts*, which is why it saved 1.7 h/day and moved coverage indicators [R9]. Most platforms lack any equivalent.
3. **Paper was never retired.** Dual documentation persists everywhere (registers as "failsafe", verification slips, signature chains). Apps added work rather than subtracting it — the central reason for the "second shift" phenomenon [R6][R8][R12].
4. **Siloed by programme and by ministry.** No cross-programme beneficiary view; no cross-app reconciliation; the worker is the integration layer [R8][R12]. Even within a state (TN: Poshan Tracker + TN ICDS), duplication was chosen over integration [R12].
5. **No decision support at the point of care.** Due lists exist; protocol guidance does not. When guidance exists (TeCHO+ risk flags), it is fixed-rule and narrow. There is no way to *ask a question* of any government platform — the interaction model is forms-in, dashboards-out. LLMs uniquely change this: natural-language, multilingual, context-assembling interaction [R16][R19].
6. **Assumptions broken by ground reality.** Always-on connectivity, English literacy, high-end devices, stable electricity, single-user ownership. Field evidence contradicts each [R8][R14].
7. **Session/security design hostile to fieldwork.** The ABHA app's 15-minute timeout with no save-state makes a 20-minute enrolment impossible in one sitting [R8]. Ni-kshay errors force full re-entry [R8].
8. **No drafting or synthesis capability.** Reports, minutes, messages, referral slips, indents, claim letters — all remain manual composition tasks. No legacy platform generates any text for the worker.
9. **Surveillance features destroy goodwill.** GPS tracks, photo-attendance, facial recognition, pay-linkage. Workers have already mobilized against these; they condition how any new tool is received [R15][R12][R14].
10. **Training and help are absent.** No in-app helpdesk; troubleshooting is social (peer WhatsApp groups); training is episodic and now often a WhatsApp video [R8]. ANMs report >50% training need on ANMOL alone [R21].
11. **Feedback loops don't close.** No referral outcome tracking, no payment-status visibility, no "why was my claim cut" explanation [R22][R10].

**What AI can do that these platforms structurally cannot:** accept messy voice/handwriting/photo input in the worker's language; assemble context across her fragmented records; generate drafts (reports, messages, slips, minutes); answer open-ended protocol questions with citations; compute schedules/scores/plans and explain them; detect her data errors before submission; and summarize circulars — all *without* requiring her to learn new forms, and all runnable offline-first on modest devices. The precedents (ASHABot, HealthVaani, SMARThealth GPT) show adoption is real when the interface is WhatsApp-like, voice-first, and local-language [R16][R17][R18].

---

## 8. Opportunity Inventory: 21 Tasks Where an AI Assistant Can Realistically Reduce Workload

Each profile answers the five required questions — **what the worker has, what's missing, what decisions she makes, what tools she uses, and why existing platforms fail** — plus the realistic AI intervention, guardrails, and precedent. Opportunities are grouped into six families and ranked within the prioritization matrix in §9.

### Family A — Documentation & Data Capture

---

#### A1. Voice-first household survey & diary digitization
**Task.** The annual/periodic household survey and continuous updates to the ASHA diary/family folders (households, eligible couples, pregnancies, births, deaths, migrations) and the AWW survey register. Currently handwritten, then often re-typed into portals. The diary itself is demonstrably hard to use — poor readability, confusing layouts, difficult retrieval (57-ASHA usability study) [R23].
**Worker has.** Deep tacit knowledge of her ~150–250 households; handwritten diary entries; verbal updates from families; prior-year survey data.
**Missing.** A structured, searchable, queryable version of her own data; time to transcribe; consistent formats across programmes.
**Decisions.** Who is new/eligible for which programme; who migrated; which households need a visit this month; how to record ambiguous information.
**Tools today.** Paper diary (4+ notebooks), pen; sometimes a personal notes app.
**Why platforms fail.** Portals capture only programme-specific slices (RCH, U-WIN, Poshan) in rigid forms; none holds the household-level "family folder" the ASHA actually thinks in; none accepts free speech; none gives her back a usable view [R8][R12].
**AI intervention.** Worker speaks after each visit ("Sunita, house 14, 6 months pregnant, second ANC done, BP high, referred to PHC"): on-device speech-to-text in her language/dialect → structured diary entry (household ID, event, dates, flags) → nightly queue for portal entry drafts (feeds A2). Retrieval becomes conversational: "Which pregnant women are due for ANC this week?" Precedent: SMARThealth GPT already shipped voice + handwriting-to-text input because ASHAs preferred audio [R18].
**Non-replacement boundary.** She still conducts the visit, judges context, owns the record; AI only captures and organizes what she already knows.
**Risks/guardrails.** Transcription errors in medical fields → mandatory confirm-back ("I recorded: 6 months pregnant, high BP — correct?"); offline-first with local storage; data stays worker-owned (she can see everything — unlike Poshan Tracker [R12]); DPDP-compliant consent; no GPS/attendance features whatsoever [R15].

---

#### A2. "Capture once, draft everywhere": multi-app entry drafting & reconciliation
**Task.** Re-entering the same events (a pregnancy registration, an immunization dose, a TB visit, a birth) into multiple siloed systems, and reconciling mismatches. Documented extreme: ~2 days for 200 Ni-kshay patient entries with error-forced re-dos [R8]; AWWs entering into Poshan Tracker *and* TN ICDS *and* paper [R12]; ASHAs working until midnight across 7 apps [R8].
**Worker has.** The authoritative event (she witnessed it); paper records; partial entries in each app; knowledge of local spelling/name variants.
**Missing.** Time; error-free transcription; a mapping between her one record and each portal's schema; visibility into which portals already hold the record (deduplication).
**Decisions.** What to enter where; how to resolve name/ID conflicts; which errors to fix first; when a portal's rejection needs a supervisor.
**Tools today.** Each app's forms; WhatsApp photos of registers to DEOs; Excel/Sheets intermediaries [R8].
**Why platforms fail.** No cross-platform write APIs exposed to workers; forms assume English literacy and uninterrupted connectivity; session timeouts destroy half-finished work [R8][R21]; even successful platforms (TeCHO+) remain single-state, single-ecosystem [R9].
**AI intervention.** From A1's structured capture, generate *draft entries* for each target app (RCH/eMamta, U-WIN, Ni-kshay, NCD portal, Poshan Tracker) via accessibility-level UI automation or state APIs where available; run pre-submission validation (mandatory fields, date logic, ID formats) and flag likely duplicates/conflicts ("Ramesh's son appears twice in U-WIN with different IDs"); batch sync when connectivity returns; keep an immutable local log so a failed upload never means re-capture. Where APIs exist (TN's PICME↔U-WIN precedent [R43]), push for direct pipes instead.
**Non-replacement boundary.** Worker reviews and submits each draft batch (one-tap confirm per record); AI never silently writes to government systems.
**Risks/guardrails.** Wrong-field mapping could corrupt official registries → human confirm step, dry-run diffs, audit log; per-app ToS compliance; start read-only + "copy-paste assistant" mode where automation is not permitted.

---

#### A3. Legacy register digitization (photo → structured data) with anomaly checking
**Task.** Converting existing paper registers (sub-centre EC/MCH registers — up to 38 per sub-centre in some states [R7]; AWW's 11 registers [R6]; ASHA family folders) into digital form during transitions (U-WIN onboarding, AAM digitization, census baseline), and spotting internal inconsistencies.
**Worker has.** Decades of paper registers; no time to type them.
**Missing.** Digitized baselines; consistency across registers (e.g., EC register vs. Poshan survey vs. RCH).
**Decisions.** Which register fields map to which portal; how to resolve conflicting dates/names; what to escalate to ANM.
**Tools today.** Manual transcription; DEO help at PHC; sometimes nothing (registers stay paper while portals stay empty).
**Why platforms fail.** They start empty and expect real-time entry; they provide no ingestion path for history; they don't cross-check across registers [R7][R21].
**AI intervention.** Camera OCR tuned for ruled Indian registers, Devanagari/Dravidian scripts, and handwriting; row/column extraction into schema; confidence-scored fields routed for quick human taps; cross-register consistency reports ("12 pregnancies in MCH register missing from EC register"; "3 children whose age conflicts between Poshan and U-WIN").
**Non-replacement boundary.** AI proposes; worker or DEO confirms each low-confidence row.
**Risks/guardrails.** OCR errors in clinical fields → confidence thresholds + mandatory review for health-critical columns; images deleted after processing or stored encrypted per DPDP norms [R32].

---

#### A4. Survey & campaign capture assistant (Census/SIR, CBAC, sickle-cell, NFHS-style)
**Task.** Door-to-door enumeration with digital forms: the 33-question Census app on overheating phones during heat-hour fieldwork [R13][R34]; CBAC household NCD+TB screening for all adults 30+ [R22]; sickle-cell mobilization/screening for a 7-crore target [R31]; 15 assorted surveys/year in Karnataka [R10].
**Worker has.** Household knowledge (she surveyed them before — often repeatedly, causing respondent fatigue [R4]); paper/app forms; her diary as a de facto pre-fill source.
**Missing.** Pre-filled answers from prior surveys (each survey starts from zero); validation in the moment; progress tracking per enumeration block; language-appropriate question wording.
**Decisions.** Whom to visit today; how to answer ambiguities; when a household needs re-visit; how to explain the survey to reluctant residents [R34].
**Tools today.** Programme-specific survey apps (often unstable), paper schedules, WhatsApp instructions.
**Why platforms fail.** Campaign apps are one-off, unusable offline in practice, English-first, and never reuse data the same worker already collected in another system [R8][R13].
**AI intervention.** (i) Pre-fill drafts from her own digitized diary (A1/A3) — worker confirms rather than re-asks, cutting door time and respondent irritation; (ii) voice Q&A capture with instant range/logic validation ("age 3 child in 'adult tobacco use' — skip"); (iii) daily block-level progress summary and re-visit queue; (iv) plain-language explainer scripts for reluctant households; (v) offline queue with automatic retry.
**Non-replacement boundary.** All household interaction, consent, and judgement stay with the worker; AI never auto-submits.
**Risks/guardrails.** Pre-fill must never fabricate answers — every pre-filled field shown as "from your diary, dated X — confirm?"; privacy: campaign data segregation from health data.

---

### Family B — Due Lists, Planning & Follow-Up

---

#### B1. Due-list generation and reconciliation (the single most repeated planning task)
**Task.** Building and maintaining due lists: pregnancies due for ANC, HBNC visits (days 3/7/14/21/28/42), HBYC visits (months 3/6/9/12/15), immunization doses per child, TB visit schedules, NCD follow-ups, adolescent registers, SAM/MAM re-measurements. The immunization handbook requires post-session left-out/dropout identification every session [R29].
**Worker has.** Her diary; ANM's session due lists (often stale); last month's lists; memory of who migrated/married/conceived.
**Missing.** A merged, deduplicated, date-computed list that reconciles portal data with ground truth; early warning of upcoming dues (next 7/30 days).
**Decisions.** Who to visit this week; whom to bring to VHND; whom to escalate as high-risk; who is a "left-out" after a session.
**Tools today.** Paper lists; ANMOL/TeCHO+/U-WIN due lists where available; WhatsApp reminders from ANM.
**Why platforms fail.** Due lists are per-silo (immunization list doesn't know the same mother is due for PNC), don't reflect migrations/duplicates, and are designed for the ANM's review meeting rather than the ASHA's daily route [R21][R9].
**AI intervention.** Nightly merge of her diary (A1) with whatever portal extracts she can access → one unified "who needs what, when" list, in her language, sorted by urgency and geography; conversational updates ("Sunita delivered yesterday at PHC — okay, I've moved her to HBNC day-3 on Sunday and flagged the newborn for HBV0 tracking"); automatic left-out/dropout detection after session-day capture.
**Non-replacement boundary.** Prioritization advice, not autopilot; she decides the route and the conversation.
**Risks/guardrails.** A missed due = a lost incentive and possibly a lost child — so the merge logic must be conservative (never drop a person present in any source; flag conflicts rather than resolve silently).

---

#### B2. Daily/weekly visit planning & route optimization
**Task.** Sequencing home visits, session days, meetings, escort trips, and Anganwadi duties across scattered hamlets — currently done in the head or on paper, with heat/monsoon constraints [R13] and no regard for the invisible evening data shift [R8].
**Worker has.** Knowledge of hamlets, household availability patterns, VHND calendar, meeting dates.
**Missing.** Time-aware scheduling that respects fixed events (session days, meetings), weather (heat-hour avoidance), battery/connectivity windows for data work, and the incentive calendar (e.g., complete HBNC day-7 within the window).
**Decisions.** What to do each day; when to batch data entry; when to request ANM accompaniment for high-risk visits.
**Tools today.** Nothing dedicated; WhatsApp instructions from supervisors.
**Why platforms fail.** TeCHO+ proved auto-generated work plans are the highest-value feature (driving its 1.7 h/day saving) [R9], but no equivalent exists outside Gujarat, and none spans Health+WCD programmes.
**AI intervention.** Weekly plan generator: "Monday: 6 HBNC visits in Wadi-2 (morning, shade hours); immunization session at AWC 11am — carry these 4 due children; evening 30-min sync of Monday's captures; Tuesday: CBAC block-3 sweep + escort Sunita to PHC…" Re-plans on voice input ("raining, postpone Wadi-2"). Includes the *data-work* budget explicitly so the second shift shrinks (batch syncing planned around connectivity windows).
**Non-replacement boundary.** Suggestions she edits; no auto-commitments to supervisors.
**Risks/guardrails.** Avoid becoming a taskmaster tool (surveillance creep [R15]); plan visible only to her unless she shares it.

---

#### B3. Immunization session support (micro-plan, tally, post-session review)
**Task.** Session-day workflow: due-list → vaccination → tally sheet → post-session review with ANM/AWW → U-WIN entry → dropout follow-up list. Cold-chain/vaccine indenting and AEFI documentation on the ANM side.
**Worker has.** Session due list, vaccine vials, tally sheets, child cards (RCH/MCP card).
**Missing.** Real-time session progress ("17 of 23 done; 4 absent; 2 refused"); instant draft of U-WIN entries; automatic dropout computation; MCP-card consistency checks.
**Decisions.** Which absentees to chase same-day; who is a defaulter vs. left-out; when to escalate refusal; vial planning for next session.
**Tools today.** Paper tally sheets; U-WIN/ANMOL post-hoc entry; MCP cards held by mothers.
**Why platforms fail.** U-WIN digitizes the registry but session-day capture remains paper-first in most blocks; adoption teething and duplication persist [R42]; no tool computes the "who didn't come and why" worklist automatically.
**AI intervention.** Voice/quick-tap session capture per child ("Ravi — pentavalent 2 — done; Meena — absent") → auto tally sheet, auto U-WIN drafts (A2), auto post-session review packet for the ANM meeting, and a chase-list with drafted call scripts for absentees; ANM side: draft vaccine indents from projected due lists + stock on hand (feeds F1).
**Non-replacement boundary.** ANM/ vaccinator confirms each child's dose record; AI never records a vaccination it didn't hear about.
**Risks/guardrails.** Immunization records are incentive-linked and audit-sensitive → confirmations, timestamps, and worker attribution for every entry.

---

#### B4. Referral loop closure & high-risk follow-up
**Task.** After referring a high-risk pregnant woman, sick newborn, SAM child, suspected TB/NCD case, the worker is supposed to track the outcome, relay advice, and complete follow-up visits. Evidence shows the loop usually never closes: only 23% of high-CBAC-score referrals reached a PHC [R22]; ASHAs report no feedback from facilities.
**Worker has.** Her referral memory/slip; the family's account of what happened (if she asks); sometimes a hospital discharge note in the family's possession.
**Missing.** Facility outcomes; structured follow-up schedules tied to each referral; prompts when feedback is overdue; simple ways to record what the hospital said.
**Decisions.** Whether the family actually went; whether to re-refer; what home care to advise post-discharge; when to alert ANM/CHO.
**Tools today.** Paper referral slips; phone calls to the facility (often unanswered); nothing systematic.
**Why platforms fail.** Referral modules exist in some state systems but feedback fields are filled by nobody; there is no patient-side or facility-side incentive to close the loop; eSanjeevani is consult-centric, not follow-up-centric [R37][R22].
**AI intervention.** Referral tracker seeded from her captures: "Sunita → PHC 12 Aug (high BP). No outcome yet — call family tonight? Here's a 3-line script." When the family returns with a discharge slip, photograph it: OCR + LLM extraction → plain-language summary in her dialect ("BP medicines started; review at PHC on 2nd; warning signs listed") → auto-schedules the follow-up visits and drafts the ANM update. Escalation rules when deadlines pass.
**Non-replacement boundary.** The human conversation with the family and the clinical re-assessment remain hers/ANM's; AI only tracks, summarizes, and prompts.
**Risks/guardrails.** Extraction errors from discharge notes → always show the original alongside the summary; never auto-close a referral.

---

### Family C — Decision Support at the Point of Care

---

#### C1. 24×7 protocol Q&A assistant ("the question she's afraid to ask")
**Task.** Answering programme/clinical/scheme questions in the moment: danger signs, ORS/zinc dosing, IFA schedules, JSY/PMMVY/Nikshay-Poshan eligibility, TB side-effects, contraceptive follow-up, "what do I do if…". Today these go to the ANM (who supervises many villages and may not know), the monthly meeting (no time for individual questions), or remain unanswered; sensitive topics (sexual health, GBV) are especially hard to raise [R16]. Pooled ASHA knowledge is only ~62–69% with weakest scores on referral-relevant danger signs [R11].
**Worker has.** Training memory (years old, often incomplete); paper job aids; ANM phone number; WhatsApp peer groups (variable quality).
**Missing.** An always-available, authoritative, private, local-language source grounded in MoHFW/ICMR/NTE/ICDS guidelines.
**Decisions.** What to advise a household; whether to refer; which scheme applies; what to tell a hesitant mother.
**Tools today.** Nothing dedicated; peers/supervisor by phone.
**Why platforms fail.** Government apps have forms, no answers; helpdesks don't exist in-app; training is episodic video content [R8].
**AI intervention.** Exactly the proven ASHABot/HealthVaani pattern: WhatsApp-like (or embedded in Poshan Tracker, as HealthVaani is), voice-in/voice-out in Hindi/regional languages, RAG over official guidelines + expert-curated FAQs, experts-in-the-loop escalation to ANM/MO for unanswered questions, private channel for sensitive queries [R16][R17][R18]. Documented effects: CHWs trusted it as authoritative, asked questions they'd hesitate to ask supervisors, and supervisors' knowledge expanded by curating answers [R16].
**Non-replacement boundary.** It advises the *worker*, never the patient directly; every answer framed as guidance for her role.
**Risks/guardrails.** Hallucination on dosages/referral criteria is the key hazard → grounded retrieval only over versioned official documents, "I don't know — asking your ANM" fallback, quarterly published error audits per protocol module and language (ORF/SAHI model [R19][R32]), kill-switch on modules exceeding error thresholds.

---

#### C2. Home-visit companion: structured walkthrough + risk flagging
**Task.** Conducting HBNC/HBYC visits, PMSMA-style ANC checks, TB home visits, and NCD follow-ups per protocol: a fixed sequence of questions, observations (respiratory rate, temperature, danger signs, feeding checks, MUAC), counselling points, and end-of-visit classification (routine / needs ANM / needs urgent referral) [R28][R47].
**Worker has.** The visit schedule (B1); her relationship with the family; training memory; a paper checklist at best.
**Missing.** Step-by-step protocol at the bedside; computation (RR by age band, CBAC score, weight-for-age); instant classification with reasons; documentation of the visit in one motion.
**Decisions.** Is this newborn sick (sepsis signs, feeding failure)? Is this pregnancy high-risk? Refer now or watch? What counselling does this mother need next?
**Tools today.** HBNC/HBYC job-aid booklets; SMARThealth Pregnancy 2 tablet app in two trial states (screening + referral support) [R18]; otherwise memory.
**Why platforms fail.** TeCHO+ flags risks but only within Gujarat's MCH silo and only from entered data [R9]; U-WIN/Poshan capture but don't guide; no platform walks a visit in the worker's language.
**AI intervention.** Conversational visit mode: ASHA taps/announces "HBNC day 3, Ravi's mother" → assistant walks the protocol as questions she asks the family, accepts spoken answers, computes classifications transparently ("RR 68 at 4 days = fast breathing → per HBNC protocol: refer to PHC now"), drafts the visit record and referral summary, and preps her counselling points. SMARThealth GPT validated demand and the audio interface for exactly this population [R18].
**Non-replacement boundary.** She performs the examination and makes the referral decision; the assistant supplies protocol recall and computation, and always shows the guideline basis. ANM/CHO/MO remain the clinical authorities (human-in-the-loop as in ORF's Sahayak design [R19]).
**Risks/guardrails.** False reassurance is the worst failure → bias toward over-referral on uncertainty; every risk output cites the guideline clause; logged for audit; error-rate monitoring by module/language; worker liability protection when protocol was followed [R19][R32].

---

#### C3. Growth monitoring & nutrition classification support (AWW+ASHA)
**Task.** Monthly weighing/height, MUAC, plotting on growth charts, classifying SAM/MAM/underweight, deciding THR/SNP adjustments, referral to NRC/health facility, and follow-up (ASHA incentive for SAM follow-up is conditional on MUAC ≥125mm) [R2]. Field reality: growth monitoring is only ~3% of AWW time; 49% of centres lacked growth charts; measurement devices are sometimes borrowed [R6][R50].
**Worker has.** Weight/height numbers, THR registers, Poshan Tracker (which computes some indicators), her knowledge of the child's household.
**Missing.** Instant plain-language interpretation with trend context ("weight flat for 3 months — not yet SAM but watch"); missing-measurement tracking; referral letter drafting; family-specific counselling (feeding practices).
**Decisions.** Classify nutrition status; refer or counsel; whom to re-measure next week; how to talk to a resistant family.
**Tools today.** Growth charts (often absent), Poshan Tracker screens, paper registers.
**Why platforms fail.** Poshan Tracker computes but doesn't coach; facial-recognition/geofence features consume the worker's attention while giving her no analytical help; TN workers can't even query their own data [R12].
**AI intervention.** Photo/voice entry of measurements → auto-plot with WHO/IAP standards → classification + trend narrative in local language → suggested actions (counselling script, referral draft, re-measure date) → child-level gap alerts ("4 children missed weighing twice"). HealthVaani's AWW training rollout (650+ workers) shows the channel works [R17].
**Non-replacement boundary.** Measurement, family engagement, and feeding decisions stay human.
**Risks/guardrails.** Misclassification → show the plotted chart and formula, not just a label; flag implausible values (weight drops of 3kg in a month) for re-measurement instead of recording.

---

#### C4. NCD screening/follow-up companion (CBAC → confirmation → treatment adherence)
**Task.** CBAC household screening (behavioural risk factors + TB symptom questions), score computation, referral of score>4, then tracking confirmed HT/DM patients on monthly drug pickups and follow-up at AAMs [R22][R51]. Evidence: coverage of forms is high (95%) but the cascade collapses — 23% referral completion, 21% diagnosis; ASHAs cite workload, stigma, and NCD-portal problems [R22].
**Worker has.** CBAC forms (paper), NCD portal (facility-entered), BP/glucose readings at AAM screening camps, patient lists.
**Missing.** Score computation and triage in the field; visibility of who got diagnosed/treated after her referral; adherence tracking; counselling content (salt, tobacco, alcohol) adapted to the household; stigma-sensitive scripts.
**Decisions.** Who to refer; how to persuade a hesitant 55-year-old to get BP checked; who needs a home BP recheck; when to alert the CHO.
**Tools today.** Paper CBAC; NCD portal at facility; WhatsApp lists from CHO.
**Why platforms fail.** The NCD portal is a facility registry, not a field tool; CBAC scoring is manual; no cascade tracking exists for the ASHA (she never learns the outcome of her referrals) [R22].
**AI intervention.** Voice capture of CBAC responses → instant score + risk explanation → referral slip draft → cascade tracker ("of your 37 high-score referrals: 9 diagnosed, 12 pending, 16 not visited — here's the chase list"); monthly adherence calendar per patient with drafted reminder messages; tobacco-cessation/IFA/diet counselling scripts in dialect; AAM-side: CHO gets AI-drafted follow-up summaries.
**Non-replacement boundary.** Diagnosis and treatment remain with MO/CHO; ASHA's role (screening, referral, adherence support) is amplified, not automated.
**Risks/guardrails.** Stigmatizing language → reviewed content templates; data minimization for sensitive conditions.

---

#### C5. TB (Ni-kshay) workflow assistant
**Task.** ASHA/TB provider duties: household contact screening prompts, referral of presumptives, treatment-initiation home visit within a week, adherence monitoring (visit/DATS-box based), side-effect watch, Ni-kshay Poshan Yojana DBT facilitation (bank linkage), loss-to-follow-up retrieval, and Ni-kshay portal entry (the documented 2-days-per-200-patients bottleneck) [R8][R44][R52].
**Worker has.** Patient list from TB unit, Ni-kshay credentials, DATS data where boxes exist, household knowledge.
**Missing.** Manageable daily worklists across her TB patients; DBT status visibility; side-effect triage guidance; relief from portal entry.
**Decisions.** Who to visit today; is this side-effect serious (hepatitis signs → urgent) or counsel-and-continue; who is defaulting; when to involve the TB health visitor.
**Tools today.** Ni-kshay portal/app (heavy), paper adherence registers, DATS platforms where piloted (valued for time savings and LTFU detection [R44]).
**Why platforms fail.** Ni-kshay is notification-centric; field usability is poor (error-forced re-entry); DBT troubleshooting is manual; no decision support for side-effects at the household level [R8][R44].
**AI intervention.** Adherence calendar with visit routes (B2); spoken visit notes → structured Ni-kshay drafts (A2); side-effect protocol Q&A grounded in NTE guidelines (C1 pattern); DBT status explainer + grievance letter drafting when payments fail; contact-screening checklists after each new case.
**Non-replacement boundary.** Clinical decisions (treatment change, serious AE management) belong to the TB unit; the AI supports the community layer only.
**Risks/guardrails.** TB data is highly sensitive → local encryption, no third-party cloud retention without DPDP-compliant processing agreements [R32].

---

### Family D — Communication & Coordination

---

#### D1. Beneficiary communication drafting (reminders, counselling scripts, rumors)
**Task.** Telling 100+ households about due services, VHND dates, THR pickup, session changes; countering vaccine/misinformation rumors; explaining schemes and DBT delays — today done door-to-door or via ad-hoc WhatsApp forwards.
**Worker has.** Phone numbers of many beneficiaries; due lists (B1); knowledge of each family's sensitivities (caste, prior refusal, language).
**Missing.** Ready, respectful, dialect-appropriate message drafts; batch-but-personized reminders; verified counter-misinformation content; time to compose.
**Decisions.** Whom to remind and how (call vs. message vs. visit); how to phrase sensitive asks (TB in family, FP counselling); which rumor needs a group meeting.
**Tools today.** Personal WhatsApp/calls on her own phone and data plan (unreimbursed) [R8].
**Why platforms fail.** Kilkari-style government mass messaging is generic, top-down, and not controllable by the worker; no platform gives her a personalizable outreach tool [R8][R12].
**AI intervention.** From due lists: draft per-benefit reminders ("Namaste Sunita-bai, Thursday is the Anganwadi weighing day; Ravi's turn — bring his card") in her dialect; voice-note generation where literacy is low; a curated rumor-response library (MoHFW-verified) with scripts; festival/weather-aware scheduling. **Drafts, never auto-send** — she approves each message, preserving her relationship ownership.
**Non-replacement boundary.** Trust is her core asset; AI must never impersonate her or bypass her judgement.
**Risks/guardrails.** Wrong medical claims in messages → content library versioned and clinically reviewed; opt-out respect; no beneficiary data sent to third-party servers beyond consented processing.

---

#### D2. Meeting copilot: agendas, minutes, action tracking (sector meetings, monthly PHC meetings, VHND/VHSND planning)
**Task.** Monthly ASHA meetings (2–3 h; attendance >90%; training + review + report/signature collection) [R48], sector meetings with ANM, VHND/VHSND planning with AWW and PRI members [R30], CDPO reviews for AWWs. Preparation and follow-through are manual: someone writes an agenda on paper, minutes rarely exist, action items evaporate.
**Worker has.** Verbal updates, paper reports, memory of last month's instructions.
**Missing.** Structured agendas tied to real data (coverage gaps, dues); minutes; an action-item tracker that surfaces "whose signature is pending on what"; pre-meeting packs so scarce meeting time isn't spent reciting numbers.
**Decisions.** What to raise at the meeting (payment delays, stock-outs, difficult households); who does what before VHND; which training topic the group needs.
**Tools today.** Paper registers, WhatsApp groups where instructions get lost [R8].
**Why platforms fail.** Dashboards serve district review meetings, not village-level working meetings; nothing produces minutes or tracks actions.
**AI intervention.** Pre-meeting pack auto-compiled from her own data (B1/A1) and supervisor-shared extracts: gaps, dues, pending signatures, incentive claim status. In-meeting: voice-recorded minutes → action items with owners/dates → follow-up nudges ("ANM signature still pending on July incentive slip"). VHND: joint checklist (who brings the due list, who mobilizes, which services, ANM/AWW/ASHA task split) — directly attacking the convergence friction documented in VHND studies [R53][R54].
**Non-replacement boundary.** Meetings remain human deliberation; AI records and reminds.
**Risks/guardrails.** Recording consent from all participants; minutes stored locally/worker-owned.

---

#### D3. Cross-cadre convergence hub (ASHA–ANM–AWW shared task view)
**Task.** The mandated-but-uninstrumented teamwork: shared beneficiary lists for VHND, division of MCH visits, joint growth-monitoring days, hand-offs when a child appears in one cadre's data and not the other's. FGD evidence: AWWs "don't know most beneficiary information"; ASHAs gather everything and feel credit is misallocated; duplicate visits and credit disputes are routine [R4].
**Worker has.** Her own records; informal WhatsApp coordination; monthly meeting contact.
**Missing.** A shared, minimal task board across the Health/WCD divide: who is visiting whom, what each knows about a household, what's pending from the other.
**Decisions.** Division of labour per household/visit; who escorts; who mobilizes for a camp; how to split credit for a completed case.
**Tools today.** WhatsApp groups, verbal agreements, paper.
**Why platforms fail.** RCH/U-WIN (Health) and Poshan Tracker (WCD) share no beneficiary layer; nothing models the *team*; state dashboards monitor cadres separately [R12][R8].
**AI intervention.** Lightweight shared list per village (opt-in by all three cadres): each worker's captures (A1) contribute events; AI deduplicates and shows "Sunita: ANC-3 done (ASHA), weighing due (AWW), VHND escort (ANM)"; conflict flags ("both of you plan to visit house 14 tomorrow"); end-of-month contribution summary usable in incentive verification disputes. Runs over WhatsApp/SMS where apps fail.
**Non-replacement boundary.** The division-of-labour negotiation stays human; AI makes the state of play visible and symmetric — reducing the informational asymmetry that fuels credit disputes.
**Risks/guardrails.** Cross-department data sharing needs a governance framework (two ministries); start with locally-brokered sharing where each worker consents per household.

---

#### D4. Circular translation & plain-language policy digests
**Task.** MoHFW/state circulars, programme guidelines, app update notices, and incentive-rule changes arrive in English/Hindi legalese via WhatsApp; workers must interpret what changed for their pay and duties (e.g., revised incentive rates, new survey mandates, Poshan Tracker feature changes) [R8][R12].
**Worker has.** Forwarded PDFs she rarely has time or language access to fully read.
**Missing.** A 5-line "what this means for you" digest in her dialect: new tasks, changed payments, deadlines, which app screens change.
**Decisions.** What to change in her routine; whether a payment cut is legitimate; what to ask at the sector meeting.
**Tools today.** Peer WhatsApp interpretations (unreliable).
**Why platforms fail.** No official channel explains circulars at worker level; training videos lag.
**AI intervention.** Ingest official circulars → verified plain-language summaries per cadre per state, with "ask about this circular" follow-up; union/facilitator-reviewed where possible. Directly counters misinformation that costs workers their dues.
**Non-replacement boundary.** Summaries link to source documents; contested interpretations escalated to facilitators/unions rather than resolved by the model.
**Risks/guardrails.** Mis-summarizing pay rules can cause real losses → human editorial review layer for payment-related digests.

---

### Family E — Reports, Incentives & Money

---

#### E1. Monthly/quarterly report assembly & drafting
**Task.** Compiling the monthly report chain: ASHA monthly activity report, ANM's MCH/monthly returns, AWW's MPR, programme-specific returns (TB, NCD, immunization), plus ad-hoc Excel/Google-Sheet returns demanded by supervisors [R8][R4][R6]. AWWs spend half an hour or more uploading a single report on patchy connections [R14]; ANMs devote a substantial slice of their 7-hour day to records/reports [R5].
**Worker has.** All source events already captured (in registers, apps, and — with A1/A2 — a local structured store); prescribed formats.
**Missing.** Automatic roll-up from events to format; validation before submission; version history; a way to answer "officer wants X by 5pm" without an all-nighter.
**Decisions.** How to classify ambiguous events; what to include/exclude; whom to ask when numbers don't reconcile.
**Tools today.** Paper → Excel/Sheets → portal; supervisor WhatsApp.
**Why platforms fail.** Each portal wants its own re-keyed aggregates; none reads from the others; none drafts the non-portal formats (the Excel/Sheets side-channel) [R8].
**AI intervention.** Report compiler: events (A1) → all required formats (MPR, monthly returns, Excel templates) with reconciliation warnings ("your immunization count is 3 higher than U-WIN — resolve before submit"); one-tap package generation; submission checklist with signature status tracking (kills the "chase the sister for signatures" loop [R4]); drafts of the narrative sections supervisors increasingly demand.
**Non-replacement boundary.** The worker certifies her numbers; AI never invents aggregates.
**Risks/guardrails.** Reports feed performance judgement and pay → full traceability from every figure to source events; no silent correction of "bad-looking" numbers (data-integrity temptation must be designed out — AI should surface discrepancies, never paper over them).

---

#### E2. Incentive claim lifecycle assistant
**Task.** The full money loop: know the rate card (~30–60 tasks, lump-sum bundles with hidden conditions [R2][R39]) → accumulate verification slips → confirm with the beneficiary that DBT arrived (ASHAs must chase women who don't volunteer it [R4]) → assemble claims → obtain signatures → track through block/district → diagnose rejections/cuts → escalate arrears. Protests across states show 3–4 month delays and unexplained cuts are endemic [R33][R34]; verification is described as "cumbersome" even in policy reviews [R10].
**Worker has.** Her activity record (with A1/E1: complete); the official rate card (poorly understood); partial payment SMS history.
**Missing.** A running ledger of "what have I earned, what's claimed, what's verified, what's paid, what's rejected and why"; deadline awareness (claim windows); plain-language explanations of bundle conditions ("full immunization ₹100 requires all doses within the first year — Ravi's DPT booster is late"); help composing grievance applications.
**Decisions.** Which claims to file this month; whom to ask for confirmation; whether a rejection is legitimate; whether to escalate collectively.
**Tools today.** Paper verification slips, bank SMS, PFMS opacity, union WhatsApp groups.
**Why platforms fail.** Incentive modules exist inside state portals but show status to officials, not explanations to workers; no tool spans claim→verify→DBT→bank; the worker is blind by design [R39][R10].
**AI intervention.** Personal incentive ledger: events → auto-mapped claims against the current state rate card; monthly claim packet with verification-slip checklist; beneficiary-confirmation prompts (D1 drafts: "did the ₹250 arrive?"); rejection diagnosis ("slip missing ANM signature for case #23") and grievance letter drafting in the correct official format; arrears summary usable in union negotiations. This is arguably the highest-trust-building opportunity: the tool visibly works *for the worker's wallet*.
**Non-replacement boundary.** She files claims and signs; AI prepares and explains.
**Risks/guardrails.** Rate cards vary by state and change — the ledger must version them and flag uncertainty rather than guess amounts; no auto-computation of "how much to demand" without citing the applicable circular (D4 integration).

---

### Family F — Logistics & Supervision

---

#### F1. Drug, vaccine & stock forecasting; indent drafting
**Task.** ASHA drug-kit replenishment (ORS, zinc, IFA, chloroquine per state kit), ANM sub-centre drug/vaccine indents and stock registers, AWW THR/SNP food-stock forecasting, AAM drug indents. Stock-outs and expiry losses are chronic; forecasting is by thumb.
**Worker has.** Consumption history in registers; last month's indent copies; knowledge of upcoming camps/session days.
**Missing.** Demand projection (e.g., next month's due-list-driven IFA need), expiry alerts, indent drafts, discrepancy detection between issued and consumed stock.
**Decisions.** What quantity to indent; what to carry for a session/camp; when a stock-out is likely.
**Tools today.** Paper stock registers; eAushadhi/logistics portals at facility level; verbal indents.
**Why platforms fail.** Logistics systems are facility-centric and don't read the field worker's forward schedule (B1/B3); WHO's digital-health guidance explicitly endorses CHW-side stock-management tools — few exist in India [R55].
**AI intervention.** From due lists and consumption: "27 pregnant women due next month → indent ~90 IFA strips; VHND on 12th → carry 20 ORS packets"; expiry warnings; photo-of-shelf stock counting where useful; indent letter/application drafts in the required format.
**Non-replacement boundary.** Physical stock management and official indents remain the worker's/ANM's.
**Risks/guardrails.** Over/under-forecasting has clinical costs → conservative defaults, human quantity confirmation.

---

#### F2. Supportive-supervision copilot (for ANMs, ASHA facilitators, Mukhya Sevikas, CHOs)
**Task.** A facilitator supervises 10–20 ASHAs with ~20 field visits/month [R38]; an ANM supervises 8–10 ASHAs plus a sub-centre; a Mukhya Sevika supervises ~25 AWWs. Their work: verify diaries/claims, spot coverage gaps, conduct on-the-job training, convene meetings, compile block reports. Today this is paper-chasing and signature-collecting, which the ASHAs experience as pressure without support [R4][R21][R28].
**Supervisor has.** Fragmented portal dashboards, paper reports, monthly meeting contact.
**Missing.** A per-worker review pack (gaps, trends, data-quality flags, training needs); a visit plan across her 15 ASHAs; time — the ANMOL study shows even high-performing ANMs cite increased workload from the app itself [R21].
**Decisions.** Whom to visit first; whose data looks wrong (error vs. fabrication — FGDs show pressure induces measurement manipulation [R4]); what training the group needs; how to resolve incentive disputes.
**Tools today.** Dashboards for officers; registers; WhatsApp.
**Why platforms fail.** Monitoring systems flag workers punitively without giving supervisors diagnostic, supportive tooling; nothing aggregates across programmes for a single ASHA.
**AI intervention.** For each supervisee: auto-compiled review pack (coverage vs. due lists, anomalies like implausible weight entries needing gentle verification rather than accusation, pending claims, training gaps inferred from Q&A usage in C1); visit scheduling across the cluster; meeting packs (D2); data-quality triage that distinguishes "likely typo" from "systematic mismatch"; escalation drafts to block level. Frees supervisor time for the coaching the system nominally wants — and indirectly reduces frontline pressure, since much ASHA stress comes from supervision-as-inspection [R4].
**Non-replacement boundary.** Supportive supervision is a human relationship; AI prepares, never judges workers autonomously. Performance-rating automation must be explicitly out of scope (surveillance red line [R15]).
**Risks/guardrails.** Anomaly flags must not become punitive by default: model outputs framed as "verify with the worker", audit-logged; worker can see her own flags (transparency as trust mechanism).

---

## 9. Prioritization Matrix

Scoring: **Impact** = time saved × frequency × error reduction × reach across cadres; **Feasibility** = data needed available locally, no dependency on unavailable government APIs, precedent exists, low regulatory risk. **Risk** = potential harm if wrong (clinical/financial).

| # | Opportunity | Impact | Feasibility | Risk if wrong | Verdict |
|---|---|---|---|---|---|
| C1 | Protocol Q&A assistant | High | **High** (proven: ASHABot/HealthVaani) | Med | **Ship first** — deployed pattern exists |
| A1 | Voice-first diary/survey capture | High | High (on-device ASR maturing) | Low | **Ship first** — foundation for everything |
| B1 | Unified due lists | High | High (uses A1 data) | Med | **Ship first** |
| E2 | Incentive ledger & claims | **Very High (trust)** | High | Med (money) | **Ship early** — fastest trust-builder |
| E1 | Report assembly | High | High | Low-Med | Ship early |
| B2 | Visit planning | High | High | Low | Ship early |
| D1 | Beneficiary message drafts | High | High | Med | Ship early (draft-only mode) |
| A2 | Multi-app entry drafting | **Very High** | Med (per-app automation limits) | Med | Stage 2 — start as copy-paste assistant |
| D2 | Meeting copilot | Med-High | High | Low | Stage 2 |
| B3 | Immunization session support | High | Med-High | Med | Stage 2 |
| C2 | Home-visit companion | **Very High (clinical)** | Med | **High** | Stage 2–3 with strict guardrails |
| A4 | Survey/campaign assistant | Med-High (spiky demand) | Med | Low-Med | Stage 2 (census window = natural pilot) |
| D4 | Circular digests | Med | High | Low-Med | Stage 2 |
| B4 | Referral loop closure | High | Med (needs OCR of slips) | Med | Stage 2–3 |
| C3 | Growth/nutrition interpretation | High | Med-High | Med | Stage 2–3 |
| C4 | NCD/CBAC companion | High | Med | Med | Stage 3 |
| C5 | TB workflow assistant | High | Med | Med-High | Stage 3 |
| F1 | Stock forecasting/indents | Med | Med-High | Med | Stage 3 |
| D3 | Convergence hub | High (systemic) | **Low-Med** (two ministries) | Low-Med | Stage 3+ — needs policy unlock |
| A3 | Legacy register OCR | Med | Med | Low-Med | On-demand (transitions) |
| F2 | Supervision copilot | High | Med | Med (labor relations) | Stage 3, co-designed with unions |

**The recommended wedge product** (smallest thing that compounds): a WhatsApp-style, voice-first, local-language assistant combining **C1 + A1 + B1 + E2** — answer protocol questions, capture visits by voice, keep her due list, keep her money ledger. None of these require government API access on day one; all four attack the highest-frequency documented burdens; and together they create the local structured data store that later stages (A2, E1, B3, C2) build on. Precedent shows demand is real: ASHABot users treated it as authoritative and asked questions they'd never ask supervisors [R16]; HealthVaani reached 800+ users and ~15k queries across 6 states in pilot and is embedded in Poshan Tracker itself [R17].

---

## 10. Design Principles & Guardrails (Non-Negotiable)

Synthesized from the failure modes of existing platforms (§7), the worker-resistance history (Shield 360, photo-attendance, Poshan mandates) [R15][R14][R12], and the governance proposals now on the table (ORF "AI Sahayak" [R19]; ABDM's SAHI strategy, Feb 2026 [R32]; WHO digital-health guidance [R55]; DPDP Act, 2023):

1. **Worker-owned by default.** The worker sees everything the tool knows about her and her beneficiaries. A tool that reports on her without serving her will be resisted as surveillance — the documented fate of prior platforms.
2. **No attendance, GPS-tracking, or performance-rating features.** Ever. Route optimization is on-device and optional; no telemetry about *where she was*, only about *what she recorded*.
3. **Voice-first, local-language-first, offline-first.** Marathi/Hindi/Tamil/Telugu/Bengali/Odia/Gujarati + major dialects; on-device ASR where possible; store-and-forward sync; battery- and data-frugal; must run on 2GB-RAM Android [R14][R8].
4. **Drafts, not actions.** Every write to a government system, every message to a beneficiary, every claim figure passes through explicit human confirmation.
5. **Grounded clinical answers only.** RAG over versioned MoHFW/ICMR/NTE/ICDS/state documents; no free generation on dosages, danger signs, or eligibility; "I don't know → escalate to ANM/expert" path with experts-in-the-loop, as ASHABot demonstrated [R16]; conservative over-referral bias under uncertainty.
6. **Published error audits + kill-switches.** Quarterly accuracy reporting by protocol module and language; automatic suspension of modules breaching thresholds; liability shield for workers who follow the tool's guidance faithfully (SAHI accountability tiering) [R19][R32].
7. **Data sovereignty & privacy.** DPDP-compliant consent and purpose limitation; health data (TB, NCD, FP) segregated and encrypted; no training on personal data without governance approval; deletion on request.
8. **Co-design with workers and their collectives.** The pile-sorting/focus-group method used for SMARThealth GPT [R18] and ASHABot [R16] is the standard: workers choose the question set, the tone, the interface. Union engagement pre-empts the surveillance reading.
9. **Reduce total work, never shift it.** Success = the second shift disappears (targets: TeCHO+-class savings of ~1.5–2 h/day [R9]); any feature that adds data entry without removing more is cut.
10. **Interoperability as policy, not heroics.** Pursue state API access (U-WIN, Poshan Tracker's HealthVaani embedding shows WCD is willing [R17][R42]); where APIs are absent, ship as an assistive layer (drafts + copy-paste) rather than fragile UI automation of official systems.
11. **Augmentation, explicitly.** Nothing automates the relational core — the home visit, the counselling, the trust. The tool makes the ASHA more of a health activist and less of a data-entry clerk, which is precisely the role erosion the evidence documents [R4][R6][R8][R10].

---

## 11. Measurement Plan

| Dimension | Metric | Baseline source |
|---|---|---|
| Time | Minutes/day on documentation, data entry, report assembly; hours of "second shift" | Time-motion re-run (Khandre/Singh/Jain protocols) [R4][R5][R6] |
| Time | ANM/DEO minutes saved (TeCHO+ benchmark: 1.7 & 1.5 h/day) | [R9] |
| Money | Days from task completion to incentive credit; claim rejection rate; arrears resolved | E2 ledger data; union surveys [R33] |
| Quality | Portal rejection/error rate; data concordance (TeCHO+ benchmark: 69→81%) | [R9] |
| Coverage | Due-list completion; immunization dropouts tracked; HBNC visit timeliness; CBAC referral completion (baseline 23%) | [R22][R29] |
| Clinical safety | Referral appropriateness audits; danger-sign recognition (pre/post vignette tests, baseline pooled knowledge 62–69%) | [R11] |
| Trust & adoption | WAU/MAU, share of visits captured by voice, refusal/attrition rates, union sentiment | ASHABot/HealthVaani engagement logs [R16][R17] |
| Harm | Error-audit findings by module/language; near-miss reports | New — required by §10.6 |

---

## 12. Realistic Deployment Paths

1. **NGO/state pilot path (0–12 months).** Partner with a state NHM/ICDS mission or a large NGO network (Khushi Baby in Rajasthan, Wadhwani AI's 6-state footprint, George Institute sites in Haryana/Telangana) [R16][R17][R18]. Ship the wedge (C1+A1+B1+E2) to 500–2,000 workers; run a stepped-wedge evaluation with time-motion endpoints.
2. **Embedding path (6–24 months).** HealthVaani's embedding inside Poshan Tracker proves platforms will host assistants [R17]. Negotiate read/draft APIs with U-WIN (national), Ni-kshay, NCD portal, state MCH apps; TN's PICME↔U-WIN linkage is the interoperability precedent to cite [R43].
3. **Public-goods path (12–36 months).** The ORF proposal — IndiaAI Mission-funded, MoHFW/NHA/MeitY-governed "AI Sahayak" with open protocol, evaluation benchmark, and certified model providers — aligns with SAHI (Feb 2026) and the India AI Impact Summit agenda [R19][R32]. A DPI-style open standard prevents fragmentation into 28 state silos, the exact failure mode of the current stack.
4. **Campaign surge path (opportunistic).** Census 2026–27 and SIR enumeration are straining lakhs of ASHAs with buggy digital tools right now [R13][R34]; a capture-and-validate assistant for enumerators (A4) is a visible, politically salient quick win — and the same machinery serves CBAC and sickle-cell campaigns [R22][R31].

**What would falsify this approach:** if pilots show that voice capture is rejected in shared-device/household-privacy contexts; if ASR accuracy in rural dialects stays below usable thresholds for medical fields; if state platforms criminalize assistive automation (ToS enforcement); or if error audits reveal clinical-answer accuracy insufficient for over-referral-biased deployment. Each is testable in a 6-month pilot, and each has at least partial counter-evidence in current deployments [R16][R17][R18].

---

## 13. Conclusion

The evidence is consistent across states, cadres, and a decade of studies: India's frontline health workforce is drowning not in care work but in the administrative shell around it — duplicate records, siloed apps, manual due lists, signature chains, incentive mazes, unexplained rejections, and a decision-support vacuum at exactly the points (danger signs, referrals, nutrition classification) where their judgement most affects survival. Existing platforms digitized the paperwork and kept the paper; they were built to watch workers, not to help them, and workers know it — hence two decades of escalating "mobile vaapsi" resistance alongside continued conscientious service.

AI assistants — voice-first, local-language, grounded in official protocols, offline-capable, and worker-owned — are the first technology generation that can plausibly absorb the *cognitive* clerical load (capture, merge, compute, draft, explain, remind) without demanding new forms, new literacy, or new trust in surveillance. The 21 opportunities above are deliberately bounded: in every one, the AI proposes and the human decides; in none does the worker become dispensable — she becomes what the programme documents always said she should be: a health activist with time to talk to the women in her village.

---

## 14. Sources

- [R1] PIB (2020). ASHA workers — state-wise numbers (NHM MIS, Sept 2019). https://www.pib.gov.in/PressReleasePage.aspx?PRID=1606212
- [R2] PIB (2020). Tasks assigned to ASHAs under NHM + ASHA incentive schedule. https://www.pib.gov.in/PressReleasePage.aspx?PRID=1606212
- [R3] CHW Central. India's ANM, AWW, and ASHA programs (numbers as of 2018). https://chwcentral.org/indias-auxiliary-nurse-midwife-anganwadi-worker-and-accredited-social-health-activist-programs/
- [R4] Khandre RR, Jakasania A, Raut A (2022/2023). "We are working for seven days a week": Time-motion study of ASHAs from central India. Med J Armed Forces India. https://pmc.ncbi.nlm.nih.gov/articles/PMC10746798/
- [R5] Singh S et al. (2018). Time-motion study of frontline health workers, South India. BMC Health Serv Res. https://pmc.ncbi.nlm.nih.gov/articles/PMC5879838/
- [R6] Jain A et al. (2020). Anganwadi worker time use in Madhya Pradesh. BMC Health Serv Res. https://pmc.ncbi.nlm.nih.gov/articles/PMC7722292/
- [R7] NHM Joint Review Mission 8 — Aide Memoire (up to 38 registers at sub-centre level). https://www.nhm.gov.in/images/pdf/monitoring/joint-review-mission/jrm-8-aide-memoire.pdf
- [R8] Chakraborty R (2026). India's Digital Health Push Is Overworking Its Front-Line Women. New Lines Magazine. https://newlinesmag.com/reportage/indias-digital-health-push-is-overworking-its-front-line-women/
- [R9] Saha S, Quazi ZS (2022). Mixed-methods evaluation of TeCHO+ in Gujarat. Front Public Health. https://pmc.ncbi.nlm.nih.gov/articles/PMC9363132/
- [R10] Singh S, Dhaliwal B, Kullu A, Sundararaman T (2024). The ASHA Program in times of UHC. RTH Resources. https://rthresources.in/conversations-on-health-policy/the-asha-program-in-times-of-universal-health-coverage-old-tensions-in-a-new-context/
- [R11] Karkala AP (2026). Protocol in Every Pocket: AI at India's Healthcare Frontline. ORF Expert Speak (citing 2025 systematic review of ASHA knowledge, PMC11724453). https://www.orfonline.org/expert-speak/protocol-in-every-pocket-ai-at-india-s-healthcare-frontline
- [R12] Raghu A (2025). From Caregivers to Data Workers: Tamil Nadu's Anganwadi workers. BehanBox. https://behanbox.com/2025-05-14/from-caregivers-to-data-workers-the-hidden-burden-on-tamil-nadus-anganwadi-workers/
- [R13] Anjali D (2026). On Census Duty, Mumbai's ASHA Workers Battle Peak Heat. BehanBox. https://behanbox.com/2026-06-09/on-census-duty-mumbais-asha-workers-battle-peak-heat-dread-monsoon-mayhem/
- [R14] Bansal V (2021). The Anganwadi angst over an unfriendly mobile app. Livemint. https://www.livemint.com/science/health/why-childcare-workers-are-suddenly-up-in-arms-11631117319254.html
- [R15] Bansal V (2021). How healthcare workers in India fought a surveillance regime and won (Shield 360). CodaStory. https://www.codastory.com/surveillance-and-control/indian-health-workers/
- [R16] Ramjee P et al. (2025). ASHABot: An LLM-Powered Chatbot to Support the Informational Needs of CHWs. CHI 2025, ACM. https://dl.acm.org/doi/full/10.1145/3706598.3713680 (see also Microsoft Research: https://www.microsoft.com/en-us/research/story/how-ashabot-empowers-rural-indias-frontline-health-workers/)
- [R17] Wadhwani AI. HealthVaani (impact data Jan 2026). https://www.wadhwaniai.org/impact/healthcare-solutions/healthvaani/ (see also Economic Times: https://m.economictimes.com/ai/ai-insights/lifting-the-floor-for-all-how-googles-gemini-models-are-powering-wadhwani-ais-healthvaani-app-for-asha-anganwadi-workers/articleshow/133374237.cms)
- [R18] George Institute for Global Health (2025). AI for Community Health Workers in India — SMARThealth GPT (BMGF Grand Challenges). https://www.georgeinstitute.org/news-and-media/news/ai-for-community-health-workers-in-india-a-bottom-up-approach-to-technology-development-part-3
- [R19] ORF (2026) — same as R11 (AI Sahayak proposal, SAHI alignment, error audits, liability, kill-switch).
- [R20] Gore M et al. (2022). ASHAs as frontline facilitators, providers, programme supporters — qualitative study, hilly Maharashtra. J Glob Health. https://jogh.org/2022/jogh-12-05052/
- [R21] Pawar N, Seth AK et al. (2026). ANM use of the ANMOL application: training-needs qualitative study. Indian J Community Med. https://pmc.ncbi.nlm.nih.gov/articles/PMC13161918/
- [R22] Mehta K, Mehta KG, Bhatt JH, Chavda P (2025). Challenges and coverage of CBAC for NCD screening by ASHAs: mixed-method study, Gujarat. Discover Public Health. https://doi.org/10.1186/s12982-025-01203-3
- [R23] Patel S, Tandon P (2025). Challenges in data documentation and retrieval in the ASHA diary: usability perspective. Soc Sci Med. https://www.sciencedirect.com/science/article/abs/pii/S0277953625007014 (summary: https://chwcentral.org/resources/challenges-in-data-documentation-and-retrieval-in-the-asha-diary-from-a-usability-perspective/)
- [R24] Assessment of Workload of ASHAs: multi-stakeholder study for task-sharing/task-shifting (2022). https://journals.sagepub.com/doi/10.1177/09720634221079084
- [R25] Prinja S et al. (2018). Cost-effectiveness of ReMiND mHealth intervention for ASHAs, UP. https://pmc.ncbi.nlm.nih.gov/articles/PMC6020234/ (program background: https://www.crs.org/sites/default/files/2025-05/strengthening-community-health-systems.pdf)
- [R26] Ward VC et al. (2020). BBC Media Action's Ananya programme (Mobile Kunji) in Bihar. https://pmc.ncbi.nlm.nih.gov/articles/PMC7758913/
- [R27] NHSRC. Better Planning of Work at Sub-Centre Level. https://nhsrcindia.org/sites/default/files/Better_Planning_of_Work_at_Sub_Center_Level.pdf
- [R28] NHSRC (2022). Handbook for ASHA Facilitators and ANM/MPW on HBNC and HBYC. https://nhsrcindia.org/sites/default/files/2022-02/Handbook%20for%20ASHA%20Facilitators%20and%20MPWs%20on%20HBNC%20and%20HBYC.pdf
- [R29] WHO India. Immunization Handbook (session due lists, left-out/dropout review). https://cdn.who.int/media/docs/default-source/searo/india/publications/immunization-handbook-1-106-part1.pdf
- [R30] NIRDPR. National Guidelines for Village Health, Sanitation & Nutrition Days. http://nirdpr.org.in/crru/docs/health/National_Guidelines_on_VHSND_English_High_Res_Print_ready.pdf
- [R31] MoHFW. National Sickle Cell Anaemia Elimination Mission (7-crore screening target; progress >7 crore). https://sickle.nhm.gov.in/home/about (see also Nair AR 2026, https://pmc.ncbi.nlm.nih.gov/articles/PMC12866030/)
- [R32] ABDM (2026). Strategy for Artificial Intelligence in Healthcare (SAHI). https://abdm.gov.in/sahi
- [R33] The Hindu (2026). ASHA workers protest in Mysuru over pay delays, incentive cuts. https://www.thehindu.com/news/national/karnataka/asha-workers-protest-in-mysuru-over-pay-delays-incentive-cuts/article70942721.ece (also New Indian Express, Bengaluru: https://www.newindianexpress.com/cities/bengaluru/2026/May/14/asha-workers-in-bengaluru-seek-rs-10000-honorarium-want-arrears-cleared)
- [R34] Times of India, Pune (2026). ASHA workers on census duty brave heat, glitches. https://timesofindia.indiatimes.com/city/pune/asha-workers-on-census-duty-brave-heat-glitches/articleshow/131365066.cms
- [R35] ThePrint (2026). Why labour laws fail India's Dalit ASHA workers. https://theprint.in/ground-reports/labour-laws-dalits-asha-workers/2944959/
- [R36] IntraHealth International. mSakhi mobile app for frontline health workers. https://www.intrahealth.org/msakhi-award-winning-mobile-phone-app-frontline-health-care
- [R37] Sood S et al. (2025). Adoption and utilization of India's eSanjeevani telemedicine platform (276M+ consults by Nov 2024). https://pmc.ncbi.nlm.nih.gov/articles/PMC12558045/ (MeitY: 481M+ patients via 140,422 AAMs, https://www.facebook.com/meityindia/posts/1337705955211839/)
- [R38] PIB (2018). Cabinet approval: ASHA Facilitator supervisory visit charges (~20 visits/month). https://www.pib.gov.in/PressReleasePage.aspx?PRID=1550451
- [R39] Jain M et al. (2022). Improving CHW Compensation: ASHA incentive design (lump-sum bundling critique). Glob Health Sci Pract. https://pmc.ncbi.nlm.nih.gov/articles/PMC9242609/
- [R40] NHM Mizoram. RCH Portal Data Entry Manual (eligible-couple registration fields). https://nhmmizoram.org/upload/RCH%20Portal%20Data%20Entry%20Manual.pdf
- [R41] Andhra Pradesh Health & Family Welfare. ANMOL program page. https://hmfw.ap.gov.in/anmol-program.aspx (case study: https://sdgcc.in/wp-content/uploads/2020/07/ANMOL-TAB.pdf)
- [R42] Gavi (2025). How two cities in India digitized vaccination status (U-WIN adoption). https://www.gavi.org/vaccineswork/how-two-cities-india-managed-digitise-vaccination-status
- [R43] Tamil Nadu Journal of Public Health & Medical Research (2025). U-WIN–PICME API linkage to reduce data entry. https://tnjphmr.com/article.php?articleid=626
- [R44] Sivashanmugam M et al. (2025). Qualitative study on digital adherence technologies for TB treatment support. https://europepmc.org/article/med/40536374
- [R45] Toppo M et al. (2025). ABHA awareness among underprivileged populations (mixed-methods). https://pmc.ncbi.nlm.nih.gov/articles/PMC12520049/
- [R46] BehanBox (2025). Why a photo-backed attendance app is distressing Maharashtra's ASHA workers. https://behanbox.com/2025-04-06/why-a-photo-backed-attendance-app-is-distressing-maharashtras-asha-workers/
- [R47] MoHFW. Home-Based Care for Newborn & Young Child operational guidelines (visit schedules; via NHSRC handbook R28).
- [R48] Capacity Building of ASHA in the Monthly Meeting Platforms in PHC and CHC in Uttar Pradesh (2020). https://www.academia.edu/41635173/
- [R49] NHM Meghalaya. Time and Motion Study of ANMs. https://nhmmeghalaya.nic.in/PDFs/Time_And_Motion_Study_of_ANMs.pdf
- [R50] SHSRC Gujarat. Evaluation of e-monitoring system (Poshan Tracker) — equipment sharing affecting data quality. https://shsrc.gujarat.gov.in/
- [R51] MoHFW. National Programme for Prevention & Control of Cancer, Diabetes, CVD and Stroke (NPCDCS) operational guidelines (CBAC/PBS). https://www.mohfw-dohfw.gov.in/static/uploads/2025/11/e69c5e28bff4da319ea13d2956def528.pdf
- [R52] Central TB Division. Ni-kshay Mitra guidance (2026); India TB Report 2024. https://tbcindia.nikshay.in/
- [R53] Sahu DP et al. (2025). Service gap assessment of VHND sessions. https://pmc.ncbi.nlm.nih.gov/articles/PMC12430925/
- [R54] Saxena V et al. (2015). Planning and preparation of VHND through convergence (ASHA/AWW/ANM/PRI). https://www.sciencedirect.com/science/article/pii/S2213398414000530
- [R55] WHO (2019). Recommendations on digital interventions for health system strengthening (CHW decision support, stock management, client registries, birth/death notification, telemedicine). https://www.who.int/publications/i/item/9789241550505

*Prepared as a research synthesis; all figures attributed to their cited sources. Access dates: October 2026.*
