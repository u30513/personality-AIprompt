# PREVENT — Personality-Informed Phishing Vulnerability Research

This is the public write-up for PREVENT, an ethics-approved research project
on why some people click phishing emails and others don't. The
implementation — OSINT collection, campaign orchestration, participant
data — is private; see [why](#why-only-a-write-up-is-public) below.

## The question

Security awareness training treats phishing susceptibility as roughly
uniform: train everyone the same way, measure the click rate, repeat.
That doesn't match how social engineering actually works — an attacker
crafting a pretext by hand instinctively adjusts it to the target. PREVENT
asks a sharper, testable version of that intuition: **does a person's
personality profile predict how they respond to a phishing attempt, and
does personalising the pretext to that profile change the outcome?**
Concretely, it looks at the correlation between demographic variables,
Big Five personality traits, self-control, and behaviour under a simulated
phishing attack.

If personality is a real, measurable factor in susceptibility, two
things follow that matter beyond the study itself: generic
one-size-fits-all awareness training is leaving a known variable on the
table, and the same personalisation technique that predicts susceptibility
could in principle be used to construct more convincing attacks. The
research is designed to produce the first finding defensively — informing
better-targeted training — while treating the second as the reason the
generation side has to stay closely held rather than openly published.

## Design, briefly

Two independent phases, deliberately kept apart so that no single dataset
links a person's personality profile to their phishing outcome outside the
research pipeline itself:

- **Phase 1** — a personality and self-control assessment (NEO-PI-R plus an
  unnamed self-control instrument), administered online. Participants are
  told only generic study aims; nothing about the phishing component is
  disclosed at this stage.
- **Phase 2** — a simulated phishing campaign, one personalised lure per
  participant, built from their Phase 1 profile plus OSINT-derived context.
  The platform records *that* a submission happened, not *what* was
  submitted, so the study gets a behavioural susceptibility measure without
  ever holding a credential. The deception is disclosed once a
  participant's involvement ends — disclosing it upfront would have
  defeated the measurement.

Favourable assessment from the university ethics committee preceded any
data collection; consent is collected once, up front, and covers both
phases. All data collection is telematic — there is no in-person stage.

## Why only a write-up is public

- The generation step is, by construction, a working method for turning a
  personality profile and public information about someone into a
  convincing, targeted phishing pretext. Publishing the pipeline — rather
  than describing it — would hand out that capability rather than study it.
- Phase 2 outcomes are tied to a deception participants did not consent to
  in advance. Nothing derived from that can be public, regardless of
  consent obtained after the fact.
- Keeping Phase 1 and Phase 2 data and tooling apart, including from public
  view, is part of what makes the ecological-validity argument hold up —
  not just a precaution layered on top of it.

## Status

Research in progress; this describes a methodology that has cleared ethics
review, not results, which don't exist yet.
