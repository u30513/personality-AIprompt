# Personality-Based System Against Spear-Phishing

**Using OSINT and Generative AI**

A research platform that measures whether a person's personality predicts how
they respond to a targeted phishing attempt — and builds the tooling needed to
test that at scale, so the finding can be turned into defence rather than left
as intuition.

> This repository is the public write-up. The implementation is private; see
> [Why the source is private](#why-the-source-is-private).

---

## The problem

Security awareness training generally treats phishing susceptibility as
uniform: train everyone the same way, measure the aggregate click rate,
repeat. That does not match how social engineering actually works. An attacker
writing a pretext by hand instinctively tunes it to the target — their role,
their interests, what they are likely to feel urgency about. The defensive
side has largely not modelled that asymmetry, because doing so requires
measuring something awkward: the person, not the payload.

This project asks a sharper, testable version of the question:

> **Does a person's personality profile predict how they respond to a
> spear-phishing attempt, and does tailoring the pretext to that profile
> change the outcome?**

Specifically, it studies the correlation between demographic variables,
Big Five personality traits (NEO PI-R), trait self-control, and observed
behaviour under a controlled phishing simulation.

If personality is a measurable factor in susceptibility, two consequences
follow. Generic, undifferentiated awareness training is leaving a known
variable unused — the same budget could be spent on the people and traits most
exposed. And the same personalisation that predicts susceptibility could be
used to build more convincing attacks, which is precisely why the generation
side of this work is held closely rather than published.

---

## How the system works

Three components, each solving a different part of the measurement problem.

### 1. Personality assessment framework

A reusable pipeline covering the full lifecycle of a psychometric instrument:
ingesting survey responses, cleaning and validating them, scoring, and
generating individual reports. Two instruments are implemented:

- **NEO PI-R** (Costa & McCrae, 1992) — the Big Five across 30 facets
- **Self-Control Scale** (Tangney et al., 2004) — a 36-item trait measure

Participants receive their own profile back confidentially; the instrument is
administered independently of the behavioural phase.

### 2. Personality inference from text

If a full psychometric instrument is required for every subject, the method
does not scale beyond a study — and an attacker certainly is not sending
questionnaires. This module trains models to predict NEO PI-R facet scores
**directly from written language**, testing whether natural text carries
enough signal to approximate a profile. It is both a research question in its
own right and the component that determines whether the broader threat model
is realistic.

A parallel line of work asks whether self-regulation capacity can be predicted
from personality facets alone, using NEO PI-R scores as features.

### 3. OSINT-informed pretext generation

The behavioural phase requires a lure that is credible to a specific person.
This component combines a participant's personality profile with
OSINT-derived personal and professional context to generate a tailored
simulation message. Safety constraints are built into the generation step
itself: output is framed as training material and must contain no active
links, no attachments, and no request for sensitive data — so a generated
message remains a simulation independently of how the delivery platform is
configured.

---

## Study design

Two deliberately independent phases, so that no single dataset links a
person's personality profile to their phishing outcome outside the research
pipeline.

| | Phase 1 — self-report | Phase 2 — behavioural |
|---|---|---|
| **What** | NEO PI-R + self-control instrument | Personalised phishing simulation |
| **Delivery** | Online questionnaire | Phishing-simulation platform |
| **Disclosure** | Generic study aims only | Deception disclosed after participation ends |
| **Output** | Individual personality profile | One behavioural record per participant, per message |

The simulation platform is configured to record **that** a submission
occurred, not **what** was submitted — yielding a susceptibility measure
without the study ever holding a participant credential.

**Ethics.** Favourable assessment from the university ethics committee
preceded any data collection. Consent is collected once, up front, covering
both phases. All collection is telematic; there is no in-person stage.
Disclosing the phishing component in advance would have destroyed the
measurement, which is why the post-participation debrief — not an upfront
warning — is the mechanism that keeps the design both valid and ethical.

---

## Why the source is private

- The generation pipeline is, by construction, a working method for turning a
  personality profile plus public information about a person into a convincing
  targeted pretext. Describing that is research; publishing it is
  distribution.
- Phase 2 records behaviour under a deception participants did not consent to
  in advance. Nothing derived from it can be public, regardless of consent
  obtained afterwards.
- Keeping the two phases' data and tooling separated — including from public
  view — is part of what makes the validity argument hold, not a precaution
  added on top of it.

---

## Credits

Built as a collaborative research project. Module authors:

- **Mathilde Lapayre** — NEO PI-R facet prediction from text
- **Virgil Rigagneau** — personality assessment framework; self-control
  prediction

With the support of IUT and Universitat Rovira i Virgili (URV).

## Status

Research in progress. This describes a methodology that has cleared ethics
review — not results, which do not yet exist.
