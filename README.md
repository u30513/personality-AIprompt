# PREVENT — Personality-Informed Phishing Simulation

This repository holds one artifact — [`prompt_template.md`](prompt_template.md)
— from a larger, ethics-approved academic study on human factors and
phishing vulnerability: *a quantitative, exploratory study of the
correlation between demographic variables, personality traits and
self-control, and individual behaviour under simulated phishing attacks.*

## Why only the prompt template is here

The study's implementation — OSINT collection, campaign orchestration,
participant data — is **not published**, for reasons that don't go away just
because the research is legitimate:

- The simulation pipeline turns a person's personality profile plus
  public/OSINT information into a targeted phishing pretext. That
  capability is dual-use by design; publishing the generation pipeline
  (as opposed to describing it) would hand out a working spear-phishing
  tool.
- Phase 2 data includes participants' behaviour under a deception they
  did not consent to in advance (disclosed only after participation, to
  preserve ecological validity) — nothing tied to that can be public,
  consented or not.
- The personality instrument (Phase 1) and the simulation platform
  (Phase 2) are run as independent sessions precisely so no single dataset
  links a person's Big Five profile to their phishing-susceptibility
  outcome outside the research pipeline.

What's safe to publish, and useful on its own, is the prompt design: how a
personality profile gets turned into a *controlled, disclosed-after-the-fact*
training message, and the safety constraints baked into that generation
step. That's this repo.

## Study design

**Two independent phases, one controlled deception.**

- **Phase 1 — self-report.** NEO-PI-R personality profile plus an
  unnamed self-control instrument, administered via Qualtrics. Participants
  are told only generic study aims at intake; each receives their individual
  NEO-PI-R profile back confidentially. Nothing about the phishing component
  is disclosed at this point.
- **Phase 2 — behavioural.** A simulated phishing campaign spread across the
  Phase 2 window, one lure per message, run on a Gophish-based platform.
  The platform is configured to record *that* a submission happened, not
  *what* was submitted — the study gets a per-participant, per-email
  behavioural record (susceptibility) without ever holding a credential.
  The deception is disclosed once a participant's involvement ends.

**Ethics & timeline.** Favourable assessment from the university ethics
committee (September 2026); informed consent is collected once, before any
data, and covers both phases. All data collection is telematic — no
in-person collection at any stage. Expected total duration: five to six
months, Phase 2 being the only variable-length stage.

## The prompt template

[`prompt_template.md`](prompt_template.md) is the generation prompt used to
produce each Phase-2 lure. It takes a participant's Big Five scores plus
OSINT-derived personal/professional context and asks for a realistic,
personalised pretext — with safety constraints written into the prompt
itself: the output must be explicitly framed as training material, and must
contain **no active links, no attachments, and no request for sensitive
data**. That constraint is what keeps a generated message a *simulation*
rather than a deliverable attack, independent of how the campaign platform
is configured.

## Status

Research in progress. This README describes methodology that has already
been through ethics review; it is not a claim about results, which don't
exist yet.
