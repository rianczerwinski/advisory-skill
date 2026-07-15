# Worked example: one design → survey → verdict → through-line

Distilled from a real run (a review of Panels + portctl, a personal
service-dashboard system). Abridged; the shape is the point.

## Input

A design brief for a workspace shell: a declarative `registry.json` drives an
iframe dashboard-of-dashboards; `portctl` supervises the services via launchd;
single-user, localhost. The ask, verbatim in spirit:

> *"what would an SME stakeholder survey say looking over this design? where would
> there be convergence? divergence?"*

## Output — Survey (diverge)

**Cast** (archetype + concern, stated first): platform/SRE (desired-state,
reconciliation) · web-platform architect (iframe composition) · security engineer
(threat model) · dev-env tooling maintainer (Procfile/Compose lineage) · UNIX
process-supervision greybeard (launchd/systemd) · suckless solo-builder · HCI
dashboard designer.

**Convergence** — each earned by differently-motivated agreement:
- *Registry-as-single-source-of-truth is the right spine.* The solo-builder blesses
  it for simplicity, the SRE for decoupling — same verdict, different reasons.
- *Iframe-persist + lazy-mount + overlay-for-health is the correct shell pattern.*
- *Single-file, zero-dep, no-build is appropriate-tech, not a shortcut* — even the
  FAANG reflex concedes once it registers "single-user localhost."
- *Use the OS supervisor* (launchd over `&`-hacks) — greybeard and SRE converge instantly.

**Divergence** — named axes, each with dissenter + steelman + rebuttal + *kind of split*:
- **Axis 1 — how much formalism a single-user system earns.** The master axis.
  Solo-builder wants hand-edited JSON forever; SRE sees no schema/locking and a
  live two-writer race. A *futures* split, not a facts split.
- **Axis 2 — build-vs-adopt (NIH).** Tooling maintainer: portctl's supervision
  half reinvents Foreman/Overmind/process-compose. Rebuttal: none of those ship
  the composition surface. Divergence narrows to a precise claim.
- **Axis 3 — the registry serves three masters** (launcher / discovery /
  dashboard-source). Highest-signal split; senior voices raise it.
- **Axis 5 — threat model.** A **values** split, explicitly: facts are agreed (an
  unsandboxed frame *can* reach neighbors); the fight is "it's localhost" vs.
  "posture regardless of scale."

**Meta-read** — collapse to the latent variable: *every divergence is a different
instrument reading the same seam — "personal tool where simplicity is the point"
vs. "infrastructure quietly accreting real services." The splits aren't independent
flaws; they're symptoms of a system crossing from the first regime toward the
second.* One root behind the many axes.

## Output — Verdict (converge)

Same axes, each collapsed to `default / challenger / flip-when`:

- **Axis 1 — formalism.** Default: stay flat (scale is conceded). Challenger:
  *not* full registry-with-TTL (distant third) — atomic-write + validate, nothing
  more; champion the SRE. Flip-when: the first *actual* clobber between the two
  existing writers.
- **Axis 2 — build-vs-adopt.** Default: keep bespoke (composition surface is the
  value). Challenger: adopt process-compose for the supervision engine, keep the
  dashboard as the skin. Flip-when: you catch yourself building log-tailing /
  crash-loop backoff / declared start-order — features those tools already ship.
- **Axis 3 — three masters.** Default: one registry + a discriminator field
  (`"ui": false`) — minimal fix for the blank-tab wrinkle. Challenger: actually
  split process-manifest from view-config. Flip-when: the *second* collision
  arrives (shown-but-not-supervised, e.g. a remote page).

**Through-line** — the defaults and flips share a shape: *every default sits on the
light pole, and every flip-condition is the second instance of a crack already seen
once* — flip on recurrence, not on principle. The axis closest to tripping is
Axis 1 (two writers on an unguarded file is a crack at 1-going-on-2).

## What made it good
- Panel cast **before** assessment; each voice a single incentive, no bios.
- Convergence tagged with *why different voices meet* — not a chorus.
- One divergence explicitly labeled **values, not facts**.
- Meta-read found the **one seam** behind six axes.
- Each challenger **narrowed to its tightest form** and **owned by a champion**.
- Each flip-condition an **observable tripwire**, never a principle.
- Ended as a **menu handed to the decider** — whose literal next move was to pick
  one ("yes do core"), i.e. it fed straight into a decision.
