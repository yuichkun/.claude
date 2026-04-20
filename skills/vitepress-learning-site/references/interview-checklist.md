# Phase 1 Interview Checklist

Use this as a question bank. You do not need to ask every question of every user — pick the ones that are actually ambiguous in their initial message. Prefer `AskUserQuestion` for decisions with multiple plausible answers; prefer plain text back-and-forth for open-ended exploration.

Pin down these dimensions before writing the plan. Open-ended topics drift; the interview's job is to commit.

## 1. Topic definition and motivation

**Why pin this down:** The motivation shapes what's "enough." Someone who wants the site as a career reference needs different depth from someone using it to unblock a specific PoC. A motivation question often unlocks a scope question.

- What is the topic, in one sentence the user would actually say?
- What triggered the decision to learn it *now*? Is there an ongoing project this supports?
- Is there an adjacent topic the user *explicitly* doesn't want to learn here (signals scope boundaries)?

## 2. Scope boundaries

**Why pin this down:** Scope drift is the #1 cause of site sprawl. If "just touch on Y" survives the interview unexamined, it will consume disproportionate effort.

- What's *in*? List the sub-topics at Part-level granularity.
- What's *out*? Explicitly — make the user say it. If they hedge ("maybe also Y?"), force a decision: commit Y or defer Y.
- Is this a single-shot build or a living reference? (Affects how aggressively to document "requires further research" gaps.)

## 3. Audience

**Why pin this down:** Determines the prerequisite floor and every initial explanation's depth. "For an engineer with Go experience but no audio background" is a very different brief from "for a musician learning to code."

- Who reads this site? (self only? team? public?)
- What do readers already know? (prior languages, domains, frameworks)
- What do readers explicitly *not* know? (this is often more useful than the positive set)
- Reading order: linear (chapters in order) or browsing (self-contained chapters)?

## 4. Content language(s)

**Why pin this down:** Affects writing style, subagent prompts, and whether to set up i18n infrastructure in VitePress.

- What language is the site written in?
- If multiple: bilingual pages? or one language per section? (VitePress i18n adds non-trivial overhead; default to single-language unless explicitly needed.)

## 5. Depth and density

**Why pin this down:** "Write me a 3-paragraph intro to X" and "write me a 20-chapter reference" are different products.

- Roughly how many Parts / chapters does the user envision? (Push back if numbers seem wildly off for scope.)
- Per chapter: skim-depth (~500 words) or spec-grade (~2000+ words)?
- For any section, what level of primary-source rigor? (Cite URLs? Quote spec language? Copy API signatures?)

## 6. Math rendering

**Why pin this down:** Math tooling in VitePress has real gotchas (see `gotchas.md`). Decide *once* upfront and configure cleanly; adding math later means reconfiguring the Vue compiler interaction.

- Will the content include mathematical notation beyond basic unicode (Σ, √, etc.)?
- If yes → KaTeX with the known-good plugin. MathJax conflicts with Vue's template compiler.
- If no → skip math setup entirely.

## 7. Diagram density

**Why pin this down:** Heavy diagram use is feasible with Mermaid but affects writing-agent prompts (diagrams as required artifacts) and page load weight.

- Will most sections benefit from diagrams, or are diagrams occasional?
- Types needed: flowchart, sequence, class, state, gantt?
- Any case for interactive visualizations beyond Mermaid (e.g., Web Audio live demos)? If yes, add complexity budget accordingly.

## 8. Bridge / application chapter

**Why pin this down:** In past engagements this was the single most useful chapter — mapping the topic being learned to the user's actual project. It forces the writing to answer "so what?" rather than stopping at explanation.

- Is there an adjacent technology, project, or context where the user will *apply* this knowledge?
- Should the site include a dedicated chapter mapping this topic's concepts to that context?
- If yes, rough axes of the mapping: concept → concept? API → API? decision table?

## 9. External audit

**Why pin this down:** The audit is Phase 8 and the best insurance against factual drift. Default to yes. Defaulting to no is reasonable only if the user is testing the skill or has time pressure.

- Run an independent audit pass at the end?
- If yes, any preference for reviewer tooling? (e.g., "use Codex if available")
- Tolerance for a second audit round if Critical/Major count is high?

## 10. Primary-source preferences

**Why pin this down:** For some topics the user already knows *the* canonical sources. Saving the writing agents time discovering them themselves is a pure win.

- Any specific specs, books, repositories, or documentation sites that should be treated as authoritative?
- Any source that should *not* be used? (e.g., "don't cite the community wiki — it's full of misinformation")

## 11. Deployment

**Why pin this down:** Deployment is optional but if it's on the user's mind, setting up config early lets them verify continuously. If it's not, don't invent it.

- Will the site be deployed, or is it local-only for the user's reference?
- If deployed: which platform?
- Expected visibility: public, private, organization-scoped?

## 12. Constraints

**Why pin this down:** Different constraints trigger different shortcuts.

- Wall-clock budget? (Affects how many parallel writing agents to dispatch vs. how deep to make each.)
- Single session or expected to span sessions? (Affects whether plan file needs to be self-contained for a future resumer.)
- Any "I already know X — skim it" instructions that can compress Part sizes?

---

## Interview anti-patterns

- **Asking everything upfront as a giant form.** Ask progressively; earlier answers re-frame later questions.
- **Accepting "I don't know" on scope.** That *is* an answer — but then the plan must reflect that the boundary is tentative, and the writing agents must be primed to flag scope drift back to the user.
- **Skipping the motivation question.** It is the most context-dense single question.
- **Confirming the plan before the user has seen it.** Write the plan file, show it, *then* ask.
- **Proposing specific libraries/tools before the user has framed scope.** The reverse is correct: scope first, then the implementation agent picks tools to match.
