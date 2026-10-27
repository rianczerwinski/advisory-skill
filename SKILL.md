---
name: advisory
description: >-
  Convene a synthetic panel of stakeholders with conflicting incentives to read
  a design, plan, rule, or decision in three modes. SURVEY maps convergence and
  divergence as named axes. VERDICT gives each axis a natural default, its
  tightest runner-up, and an observable flip condition. OBJECTION surfaces the
  strongest adversarial cases. Use when the user asks what an SME or stakeholder
  panel would advise, says "call/check the advisory panel," "consult AP," "ask
  AP," "AP verdict," "AP survey," "AP objections," or any phrase where AP stands
  for the advisory panel; asks where experts converge and diverge; wants the
  most natural option and next-best competitor; asks when the alternative would
  be preferable; or says "find the objections."
  Produces a decision menu rather than pretending the simulated panel is an
  authority; its axis verdicts can feed tee-up and its survey pairs with §equip.
license: MIT
---

# advisory

Read a design, plan, or decision **the way a panel of real subject-matter experts would** — then hand back not a verdict but a structured map the decider can act on. The panel is a *lens*, not an authority: it exists to surface the considerations a single view would miss, never to decide for you.

The construct runs a natural diverge→converge arc, and the three modes are three cuts of the same panel:

- **Survey** (diverge) — where do the experts agree, where do they split, and *along which axes*. Output: convergence list + named divergence axes + a meta-read.
- **Verdict** (converge) — reuse those axes; collapse each to `default / runner-up / flip-when`. Output: a per-axis decision menu.
- **Objection** (adversarial) — the panel as devil's advocate: the strongest case *against* a proposal or rule. Output: ranked objections, each owned by the voice that raises it.

Survey generates the axes; verdict consumes them. In practice the verdict feeds straight into a decision — hand it to `tee-up` to serialize, or to `§equip` as the mapped landscape.

## Hard constraint: a panel that agrees with itself is worthless

The one failure that voids the whole method is **the panel collapsing into a single voice wearing many hats.** LLM persona simulation has a documented, counterintuitive failure — *persona manifold collapse*: the more elaborately you specify each expert, the more their outputs converge toward one average voice, and over a long response the model drifts back to its default "agreeable assistant" and validates whatever it's reviewing. So the discipline is structural, not decorative:

- **Cast by conflicting incentive, not by biography.** A voice is defined by *what it optimizes for and what it fears* (the SRE fears silent drift; the solo-builder fears lost simplicity), not by a backstory. Minimal distinguishing detail — elaborate bios *cause* the collapse.
- **Convergence counts only when differently-motivated voices agree.** "The solo-builder and the SRE both bless the registry — one for simplicity, one for decoupling" is real convergence. Seven voices agreeing for the same reason is the model's single opinion in costume; report it as one voice, not seven.
- **Every divergence axis must name a real dissenter and the condition under which the design is wrong.** If no voice can mount a genuine objection, you have sycophancy, not consensus — say the panel found nothing, don't manufacture a split.

This is load-bearing. Full grounding and the empirical findings are in [references/methods.md](references/methods.md).

## Casting the panel

Name the room **before** any assessment — a position is meaningless without its holder. For each design, pick the 4–8 archetypes whose incentives genuinely pull in different directions on *this* object, and state each one's concern in a few words. Prefer real professional/subcultural stances (platform-SRE, security engineer, suckless solo-builder, HCI designer) over generic "optimist/pessimist." If the design sits in a field the model knows only thinly, **say so and thin the panel** rather than fabricating credible-sounding experts — a confabulated panel is worse than a small honest one.

## The three modes

### Survey (diverge)
1. **Cast** the panel (above), archetype + concern each.
2. **Convergence** — the near-unanimous agreements, each tagged with *why differently-motivated voices land together*.
3. **Divergence** — organized into **named axes**, not a flat list. Per axis: the fault line, the dissenter who raises it, the steelman, the rebuttal. Discriminate the *kind* of split — a **facts** split ("is this actually exploitable?") is not a **values** split ("posture regardless of scale").
4. **Meta-read** — collapse the surface axes to the one latent variable behind them where one exists ("every split is an instrument reading the same seam: personal-tool vs. accreting-infrastructure"). This is the highest-value move; do it when the axes genuinely share a root, skip it when they don't.

### Verdict (converge)
Reuse the survey's axes. For each, in a self-contained line:
- **Default (natural):** the center of gravity, + which voices concede it.
- **Challenger:** the *tightest* runner-up — narrow it ("not the full registry-with-TTL, that's a distant third; it's atomic-write + validate, nothing more"), and name its champion voice.
- **Flip-when:** the concrete, **observable tripwire** that would move you to the challenger — an event you can watch for ("the first time two writers clobber the file"), never a principle ("if you value robustness").

Close with a **through-line** if the defaults or flip-conditions share a shape ("every flip is the second instance of a crack seen once").

### Objection (adversarial)
The panel pointed at refutation: the strongest objections to a proposal, design, or proposed *rule*. Rank by force; attribute each to the voice that raises it; steelman before you answer. Devil's advocacy skews negative by design (that's its job) — don't average it back into blandness, but do separate objections that *kill* the proposal from those that merely *bound* it.

## When to use
- A design/plan/decision is on the table and you want the spread of expert reaction, or the per-axis default-and-runner-up, or the strongest objections.
- The user says any of the description's trigger phrases ("what would an SME survey say", "check the advisory panel", "what does the advisory panel say", "next-best option and when I'd prefer it", "find the objections").
- Another skill needs a design reviewed before a decision (`§equip` landscape, `tee-up` intake).

## When NOT to use
- **A real SME is reachable.** Simulating a panel you could just *ask* is a downgrade — use `elicit` on the actual expert.
- **The domain is outside the model's grounding.** Better a disclosed gap than a fabricated panel (see casting).
- **You need calibrated probabilities.** The panel surfaces considerations; it does **not** estimate likelihoods. Convergence is not evidence of correctness — it can be the model's own prior in costume ([references/methods.md](references/methods.md), honest scope).
- **It's engineering-lens code review of an existing codebase** — that's `audit-planes` (fixed product-agnostic planes), not a cast panel of stakeholders.

## Composition
- **→ tee-up.** Each axis-verdict (`default / runner-up / flip-when`) is already a normalized decision; hand the set to `tee-up` to serve one at a time.
- **→ §equip.** The survey *is* a mapped decision landscape; when the user is equipping to decide, deliver the survey and stop short of a recommendation.
- **vs. audit-planes.** audit-planes projects fixed engineering planes onto code; advisory casts stakeholder voices onto a design. Different object, different lens.
- **uses elicit.** When the verdict needs a preference the model can't infer, ask via `elicit`'s fork-based, strawman-first style — don't route a knowledge gap to the user as a fork.

## Anti-patterns
See [antipatterns.md](antipatterns.md) — wrong→right pairs drawn from the documented failure modes (fake convergence, persona over-specification, sycophantic panel, strawman runner-up, flip-condition-as-principle, values/facts confusion, delivering a verdict instead of a menu, fabricated panel, convergence-as-calibration).

## Additional resources
- [references/methods.md](references/methods.md) — prior art (Delphi, dialectical inquiry vs. devil's advocacy, nominal group technique, premortem, six hats, wisdom-of-crowds/diversity), the LLM persona-collapse findings, and the honest-scope boundary.
- [examples/panel-survey.md](examples/panel-survey.md) — a full worked run: one design → survey → verdict → through-line.
