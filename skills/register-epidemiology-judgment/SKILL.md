---
name: register-epidemiology-judgment
description: >
  Danish and Nordic register-epidemiology judgment for the lab. Use for register-based cohort
  analysis, ICD-coded outcomes, prescription-registry or pharmacoepidemiology work, CPR
  linkage, or competing-risks analysis in register data. Some calls are lab-specific fill-ins
  to confirm.
---

# Register Epidemiology Judgment

Decisions, not a registers manual. Where a choice is the lab's own it is marked LAB CALL;
confirm it with the lab. Report what a design cannot see rather than assuming it away.

## The registers

The Danish system links on the CPR number across national registers: the patient and hospital
registry, the prescription registry, the cause-of-death registry, and disease-specific and
cohort resources. Each has a coverage start date, a completeness profile, and a validity that
varies by diagnosis.

LAB CALL: which registers and cohorts the lab actually uses (for example the patient registry,
prescription registry, DanThyr, DBDS as a blood-donor cohort), and the access route for each.

## Study design

- Prefer a new-user (incident-user) design over a prevalent-user design. Prevalent users are a
  survivor population, already selected for tolerating the exposure.
- Immortal time bias is the classic register trap: time between an index date and the first
  qualifying event during which the outcome could not occur, misassigned to the exposed group.
  Define the index date so no immortal time leaks in, or use a landmark or time-varying design.
- Confounding by indication: people prescribed a drug differ from those not prescribed it for
  reasons tied to the outcome. An active-comparator design (compare two drugs for the same
  indication) controls much of it; a comparison against non-users usually does not.
- The healthy-adherer effect: adherence correlates with health behaviors the registers do not
  capture, so adherence looks protective for outcomes it has no mechanism to affect.

LAB CALL: the lab's standing design defaults (new-user, active-comparator, landmark).

## Coding drift and validity

- ICD coding changed over time (the ICD-8 to ICD-10 transition in Denmark) and coding practice
  drifts even within a version. A diagnosis code does not mean the same thing across decades.
- Registers have start dates and completeness that vary; a "zero" before a register began is
  missing, not absent disease.
- Do not assume a coded diagnosis is correct. Use published validation studies for the
  positive predictive value of the specific code, and cite them. Where no validation exists,
  say so and treat the outcome as measured with error. LAB CALL: the outcome validation studies
  the lab relies on for the codes it uses most.

## Time and censoring

- Define the index date deliberately and identically across groups.
- For competing events (death competes with a non-fatal outcome), Kaplan-Meier overestimates
  cumulative incidence. Use cause-specific hazards and the cumulative incidence function, and
  report competing-risks results, not a naive survival curve.
- Handle left-truncation, and censor at emigration and death. Emigration is real loss to
  follow-up in Danish data and must be modeled.

## Confounding and what registers miss

Registers usually lack lifestyle, BMI, smoking, alcohol, and socioeconomic detail beyond
proxies. Name the unmeasured confounders explicitly. Use negative-control outcomes or exposures
to detect residual confounding, active-comparator designs to reduce it, and sensitivity
analyses (including a quantitative bias analysis where it matters) to bound it.

## Ethics and access

Register access runs through approvals and is analyzed on secure servers with no data export.
Permissions, notification or approval bodies, data-source pricing, and legal review all gate a
project and take time.

LAB CALL: the specific approval and access path the lab uses, the notification and cost steps
to build into a project timeline, and any data-source-specific constraints.
