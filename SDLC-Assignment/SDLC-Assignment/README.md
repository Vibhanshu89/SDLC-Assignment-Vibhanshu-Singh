# SDLC-Assignment-Vibhanshu Singh
## Smart-Attend — Student Attendance App
### Course: SDLC & DevOps Fundamentals | Role: Junior Project Manager

---

## Project Overview

**Smart-Attend** is a university startup mobile application that uses **Geo-fencing** to automatically mark student attendance when they enter a classroom. Midway through development, a new requirement was added by the Dean: **Biometric (Face ID) Verification** to prevent proxy attendance.

This repository contains the SDLC analysis, sprint planning, and backlog artifacts for the project, managed using the **Scrum Agile Framework**.

---

## Repository Contents

| File | Description |
|------|-------------|
| `SmartAttend_Analysis.docx` | Full analysis: Waterfall failure, Agile pivot, Sprint plans |
| `Sprint_Backlog_SmartAttend.xlsx` | Sprint 1 & Sprint 2 backlogs + full Product Backlog |
| `README.md` | This file — includes CI/CD explanation |

---

## Why CI/CD Is Used to Push Sprint Updates to Students Automatically

### What is CI/CD?

**CI/CD** stands for **Continuous Integration / Continuous Deployment**. It is a DevOps practice that automates the pipeline of building, testing, and deploying software every time a developer commits new code to the repository.

In the context of **Smart-Attend** and our 2-week Scrum Sprint cycle, CI/CD plays four critical roles:

---

### 1. Continuous Integration (CI) — Catching Bugs Between Sprints

Every time a developer pushes code to the `main` or `develop` branch (e.g., after completing US03 — the Geo-fencing logic), the CI pipeline:

- Automatically runs all **unit tests** and **integration tests**
- Checks **code coverage** (minimum threshold: 80%)
- Runs a **security scan** on sensitive modules (especially the Face ID / biometric pipeline)
- Reports pass/fail status before the code is merged

This ensures that Sprint 2's new Face ID feature does not accidentally break Sprint 1's Geo-fencing or Login features.

**Tools Used:** GitHub Actions (pipeline), Jest (unit tests), SonarQube (code quality)

---

### 2. Continuous Deployment (CD) — Pushing Updates to Students Automatically

Once CI passes all checks, the CD pipeline:

- Builds the app bundle automatically (`.ipa` for iOS, `.apk`/`.aab` for Android)
- Pushes the new build to **Firebase App Distribution** for beta testers (internal students/teachers)
- At Sprint completion, triggers a submission to the **Apple App Store** and **Google Play Store**

Students who have Smart-Attend installed **receive the update automatically** — they do not need to manually download a new version. This mirrors how apps like WhatsApp or Google Maps push updates seamlessly every few weeks.

---

### 3. Enabling Rapid Sprint Releases

Our sprint cycle releases two major versions:

| Sprint | Release Contents | CI/CD Trigger |
|--------|-----------------|---------------|
| **Sprint 1** (End of Week 2) | Login + Geo-fencing + Notifications + Teacher Dashboard | Merge to `release/sprint-1` branch |
| **Sprint 2** (End of Week 4) | Face ID + Enhanced Reporting + Admin Override | Merge to `release/sprint-2` branch |

Without CI/CD, each release would require manual build steps, manual testing sign-offs, and manual store submissions — taking days. With CI/CD, the entire process completes in under **2 hours**.

---

### 4. Quality Gates — Protecting Biometric Security

The CI/CD pipeline enforces **quality gates** that block deployment if:

- Any test fails
- Code coverage drops below 80%
- A **security vulnerability** is detected in the biometric data handling code (e.g., if facial data is accidentally sent to a server instead of being processed on-device)
- Linting errors or code style violations are present

This is especially critical for the **Face ID module**, where a single security flaw could expose sensitive biometric data of thousands of students — a serious privacy violation under GDPR and India's PDPB.

---

### CI/CD Pipeline Diagram

```
Developer Pushes Code
        │
        ▼
┌───────────────────┐
│  GitHub Actions   │  ← CI Triggered on every push
│  (CI Pipeline)    │
│  ─ Run Tests      │
│  ─ Coverage Check │
│  ─ Security Scan  │
│  ─ Lint Check     │
└────────┬──────────┘
         │ All Checks Pass
         ▼
┌───────────────────┐
│  Build App Bundle │  ← CD Stage 1
│  (.ipa / .apk)    │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  Firebase Distrib │  ← Beta release to testers
│  (Internal Beta)  │
└────────┬──────────┘
         │ Sprint End Approval
         ▼
┌───────────────────┐
│  App Store / Play │  ← Production release to students
│  Store Submission │
└───────────────────┘
```

---

## Sprint Summary

### Sprint 1 — MVP (Weeks 1–2)
**Goal:** Working, testable app with Login, Geo-fencing, and Core UI

| Task ID | User Story | Priority | Est. Hours |
|---------|-----------|----------|-----------|
| US01 | Student login via university ID | High | 4 |
| US02 | Teacher views real-time attendance list | High | 6 |
| US03 | System detects student within 10m | High | 8 |
| US04 | Student receives attendance notification | Medium | 3 |
| US05 | Admin manually overrides attendance | Low | 4 |

**Total: 25 hours**

---

### Sprint 2 — The Update (Weeks 3–4)
**Goal:** Biometric Face ID integration + Dashboard refinement

Key deliverables:
- Face ID verification (iOS + Android)
- Anti-proxy logic (Geo-fence AND Face ID both required)
- On-device biometric processing (never stored server-side)
- Enhanced reporting dashboard with CSV export

---

## Waterfall vs Agile — Why We Switched

| Issue | Waterfall Problem | Agile (Scrum) Solution |
|-------|-----------------|----------------------|
| **Rigidity** | Cannot revisit requirements once development starts | Backlog updated every sprint — new features welcomed |
| **Cost of Change** | Late changes cost 10–100x more than early changes | Incremental builds keep change cost low |
| **Delayed Testing** | Testing only at month 5–6 of a 6-month cycle | Every sprint includes dev + testing |

---

## Tech Stack

- **Frontend:** React Native (iOS + Android)
- **Backend:** Node.js + Express
- **Database:** PostgreSQL
- **Geo-fencing:** Google Maps Geofencing API / Apple Core Location
- **Biometrics:** Apple Face ID (LocalAuthentication) / Android BiometricPrompt
- **CI/CD:** GitHub Actions + Firebase App Distribution
- **Testing:** Jest + Detox (E2E)

*Assignment Submission — SDLC & DevOps Fundamentals*
*Student: Vibhanshu Singh | REG NO. 12314921 | Deadline: 14 March 2026*
