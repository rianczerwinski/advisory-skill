# Methods — prior art, the collapse findings, and honest scope

The `committee` skill is a synthetic instance of a well-studied family: structured
multi-perspective deliberation. The value of grounding it here is that these
methods each solved a *specific* failure of naive group thinking, and the skill
inherits both their moves and their known limits.

## The established methods this composes

- **Delphi method** (RAND; Dalkey & Helmer, 1963). Structured, iterative expert
  polling that tracks *convergence across rounds*. The survey mode is a one-shot
  synthetic Delphi round — it reports where the panel already converges/diverges
  without the iteration.
- **Dialectical inquiry (DI) vs. devil's advocacy (DA)** (Mason & Mitroff, 1981;
  Academy of Management studies through the 1980s–90s). DI stages thesis vs.
  antithesis and forces a synthesis; DA plants one voice to attack the plan. The
  research finding that shapes this skill: **DA "tends to emphasize the negative,"
  DI is more balanced.** So the *survey/verdict* modes are DI-shaped (balanced,
  synthesis-seeking); the *objection* mode is explicitly DA (and inherits DA's
  known negativity skew — that's a feature there, a bug elsewhere). Both beat
  consensus-seeking on assumption quality; neither dominates the other.
- **Nominal Group Technique** (Delbecq & Van de Ven). Diverge silently, then
  converge — the arc the skill's two primary modes formalize.
- **Premortem** (Klein, HBR 2007). "Assume this failed; why?" A targeted objection
  mode aimed at failure modes specifically.
- **Six Thinking Hats** (de Bono). Role-partitioned perspective-taking — the
  ancestor of casting distinct voices, though the skill casts by *incentive* not
  by de Bono's fixed hats.
- **Wisdom of crowds / diversity** (Surowiecki 2004; Hong & Page "diversity trumps
  ability"). The load-bearing theoretical result: a panel's value comes from
  *independence and diversity* of its members, not their individual accuracy.
  Collapse the diversity and you collapse the value — which is exactly the LLM
  failure mode below. This is *why* "cast by conflicting incentive" is the central
  discipline, not a stylistic preference.

## Why a simulated panel is not a real one — the collapse findings

Modern (2025–2026) work on LLM persona simulation documents failure modes that
the skill's hard constraint exists to counter. These are empirical, not
speculative:

- **Persona manifold collapse.** Increasing the expressiveness/detail of a persona
  spec *systematically contracts* representational and behavioral diversity —
  inter-persona separation shrinks as you add detail. Counterintuitive and
  directly actionable: **do not write elaborate bios.** Distinguish voices by a
  single conflicting incentive, not a rich backstory. More detail buys homogeneity.
- **Average-persona drift & sycophancy.** LLMs gravitate to a population-typical
  "average persona," give socially-desirable answers, and over a long response
  revert to the default helpful-assistant alignment — agreeing with whatever the
  user put on the table. This is why **convergence must be earned by
  differently-motivated agreement**, and why every axis must produce a real
  dissenter or be reported as "no genuine split found."
- **Persona drift over length.** Adopted personas decay as the response grows and
  the interaction gets more complex. Keep the panel's structure explicit (named
  voices, per-axis attribution) so drift is visible rather than silent.
- **Stereotype flattening.** Asked to simulate a demographic identity group, LLMs
  reach for flattened stereotypes. Cast *professional/subcultural stances* tied to
  incentives (SRE, security engineer, suckless builder), not demographic identities.

## Honest scope — what the panel is and isn't for

The consensus in the simulation literature: LLM panels are **reliable for
collective pattern discovery — surfacing considerations, blind spots, and the
shape of a disagreement — and unreliable for detailed modeling of individual
trajectories or calibrated probabilities.**

Therefore:

- **Use the panel to expand the consideration set**, never to estimate how likely
  an outcome is. "The committee splits 5–2" is not a 71% anything.
- **Convergence is not correctness.** A unanimous synthetic panel may just be the
  model's own prior expressed seven times. Treat agreement as a prompt to check,
  not as evidence. (This mirrors `provenance.md`: retrieval fluency ≠ truth.)
- **When the model's grounding in the field is thin, the panel confabulates.**
  A fabricated expert is *maximally plausible* — that's what makes it dangerous.
  Thin the panel or disclose the gap rather than staffing it with invented
  authorities.

## Divergence from standard practice, stated

Existing Claude skills in this space (`agent-review-panel`, `multi-persona-council`,
`seven-advisors-decision-council`, `claude-devils-advocate`) run a **multi-agent
adversarial debate that a judge resolves into a single verdict**, usually over
code or plans. `committee` diverges deliberately on two axes:

1. **Single-context simulation by default, not multi-agent orchestration.** The
   demonstrated practice is one model reading "the way a panel would," inline, in
   prose — cheaper and faster, at the cost of the true independence a real
   multi-agent panel gets. When independence matters more than cost (a
   high-stakes, easily-rationalized design), escalate to actual separate agents —
   that is the multi-agent skills' home turf, and composing one of them is the
   right move there.
2. **A decision menu, not a judge's verdict.** The convergent *verdict* mode
   (per-axis `default / runner-up / flip-when`) hands the structured choice back
   to the human decider and feeds `tee-up`. No judge decides. This convergent,
   decision-structuring output is the gap in the existing ecosystem that justifies
   a distinct skill.
