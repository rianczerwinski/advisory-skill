# Anti-patterns

Every trap below is a wrong→right pair with the single discriminating feature that
flips it. Most are the observable signature of one root failure — the panel
collapsing into a single agreeable voice ([references/methods.md](references/methods.md)).

### Fake convergence (agreement for one reason)
❌ Wrong: "All seven voices agree the registry is the right spine." (Seven hats, one head.)
✅ Right: "The solo-builder and the SRE both bless the registry — one because it's simple, one because it's decoupled. Differently-motivated, so the agreement is real."
Why it flips: convergence is only signal when the voices that meet were pulling in *different* directions; same-reason agreement is the model's single opinion multiplied.
Prevents: reporting the model's own prior as a unanimous expert consensus.

### Persona over-specification
❌ Wrong: "Marcus, 43, ex-Google SRE, three kids, runs marathons, believes in…" (a novel per voice).
✅ Right: "The SRE voice: optimizes for reconciled desired-state, fears silent drift." (Incentive + fear, nothing more.)
Why it flips: elaborate bios *cause* persona-manifold collapse — added detail contracts diversity. A voice is its conflicting incentive, not a backstory.
Prevents: seven richly-drawn personas that all say the same thing.

### Sycophantic panel
❌ Wrong: A review where every axis ends "…and this is handled well," no dissenter anywhere.
✅ Right: Every divergence axis names the voice that objects and the condition under which the design is wrong — or the panel reports "no genuine split found here" explicitly.
Why it flips: a panel that can't mount an objection isn't converging, it's the default helpful-assistant validating the user; real review produces real dissent or an honest null.
Prevents: an agreeable rubber-stamp dressed as expert scrutiny.

### Strawman runner-up
❌ Wrong: "Default: keep it. Runner-up: throw it all out and rewrite in Rust." (A weak challenger that flatters the default.)
✅ Right: "Runner-up: not the full registry-with-TTL (a distant third) — it's atomic-write + validate, nothing more. Champion: the SRE voice."
Why it flips: the honest runner-up is the *tightest* real competitor, narrowed and owned by a champion; a strawman exists only to make the default win.
Prevents: a decision menu that pretends there's no real alternative.

### Flip-condition as principle, not tripwire
❌ Wrong: "Flip to the challenger when robustness matters more than simplicity."
✅ Right: "Flip the first time two writers actually clobber the file — an event you can watch for."
Why it flips: a principle is unfalsifiable and always half-true; a tripwire is an observable event that either fires or doesn't, so it's actually decidable later.
Prevents: a "switch-condition" the decider can never tell has been met.

### Values-split mislabeled as facts-split (or vice versa)
❌ Wrong: "The panel disagrees on whether the iframe threat is real." (Framed as one fight.)
✅ Right: "Facts are settled — one compromised frame *can* reach its neighbors. The split is values: 'it's localhost, don't bother' vs. 'posture regardless of scale.'"
Why it flips: naming the kind of split tells the decider whether more *investigation* (facts) or a *priority call* (values) resolves it — different actions.
Prevents: researching a values disagreement forever, or voting on a matter of fact.

### Verdict instead of a menu
❌ Wrong: "The panel has decided: keep it bespoke. Moving on."
✅ Right: "Default is keep-bespoke; challenger is adopt-the-engine-keep-the-skin; flip when you catch yourself building log-tailing. Your call."
Why it flips: the panel is a lens, not an authority — its job is to structure the choice (default/runner-up/flip) and return it, not to make it. A judge's verdict is a *different skill* (`agent-review-panel`).
Prevents: laundering the model's pick into "what the experts decided."

### Fabricated panel in a thin domain
❌ Wrong: Staffing a full seven-voice panel of "leading experts" on a niche the model barely knows.
✅ Right: "I can ground maybe two of these voices; beyond that I'd be inventing authorities. Here's the thin-but-honest panel, and where a real SME is needed."
Why it flips: a confabulated expert is *maximally plausible* — the fabrication is undetectable from inside, so honesty about grounding is the only guard.
Prevents: a credible-sounding panel that is entirely the model's imagination wearing credentials.

### Convergence read as calibration
❌ Wrong: "The panel is 6–1 in favor, so this is very likely the right call."
✅ Right: "The panel leans 6–1 — which tells you the consideration is one-sided, not that the outcome is 86% likely. Treat the lean as a prompt to check the lone dissenter's case."
Why it flips: the panel surfaces the *shape* of a consideration, never a probability; a vote count is not a likelihood and unanimity is not proof.
Prevents: turning a qualitative reading into a false quantitative confidence.
