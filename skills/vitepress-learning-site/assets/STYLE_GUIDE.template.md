---
title: "Style Guide (for writers)"
---

# Style Guide (for writers)

> Template: copy this file into `docs/STYLE_GUIDE.md` in the generated site, then customize sections 1, 2, 9 (and any others) to match Phase 1 decisions. Sections 3, 4, 5, 6, 7, 8, 10, 11, 12 should stay mostly intact — they encode the fact-first discipline.

Every page in this site is written according to this guide. Writing sub-agents must read it before touching any content. External auditors will evaluate pages against it.

## 1. Audience and assumptions

<!-- FILL FROM PHASE 1: audience profile. Include what readers are assumed to know and what they are explicitly not assumed to know. -->

## 2. Voice and tone

- <!-- FILL: formal / conversational / academic / neutral-technical -->
- Neutral prose. No emojis. No marketing-style enthusiasm or emotive adjectives ("amazing", "powerful", "elegant").
- No time-relative phrasing ("now", "recently", "previously", "new", "old", "used to"). Describe what the code/system does, not how it evolved.
- Readers come to learn the topic, not the author's feelings about the topic.

## 3. Fact-first discipline (the core rule)

This is non-negotiable. Auditors enforce it.

- Before making any factual claim, consult the primary source: specification, official documentation, source headers, standard textbook. Use a web-fetching tool (or equivalent) to load the source — do not write from memory.
- API names, signatures, quoted spec text, constant values, and version numbers must be **verbatim** from the primary source.
- When a claim cannot be verified against a primary source, mark it inline with a localized equivalent of:

  > NOTE: unverified — needs confirmation

  The English phrase `NOTE: unverified` must appear literally (even in non-English content) so auditors can grep for it.

- Secondary sources (blog posts, Stack Overflow, community wikis, Wikipedia) do not ground factual claims on their own. Wikipedia is acceptable as a navigation aid to find primary sources.

## 4. Source citation

Every Markdown file in `docs/` ends with a `## Sources` section (localize heading text if appropriate — e.g., `## 参照ソース` in Japanese content; keep the structure identical).

Format:

```markdown
## Sources

- [Page title — specific section](https://vendor.com/docs/section#anchor)
- `path/to/source/file.h` (at commit SHA or tag)
- Book author, *Book Title*, edition, pages X–Y
- Spec name, §X.Y (https://example.org/TR/spec/)
```

Rules:

- Deep-link. Top-page URLs (`vendor.com/`) are insufficient.
- For source repositories, include a commit SHA or tag in the URL (not floating `main`) unless the project is actively being rev'd.
- For books, include edition and page numbers where possible.

## 5. Heading hierarchy

- `#` = page title. One per file. Matches frontmatter `title` exactly.
- `##` = major section.
- `###` = subsection and figure titles.
- `####` and below: avoid. If needed, consider splitting to a new subsection.

## 6. Code blocks

- Always include a language tag: `cpp`, `ts`, `js`, `py`, `rs`, `go`, `json`, `yaml`, `bash`, `text`, `mermaid`, etc.
- For excerpts from source files or specs, put the source path in a leading comment so the origin is unambiguous:

  ```cpp
  // path/to/file.h (at SHA xxxxxxx)
  class Foo {
    void bar();
  };
  ```

- Do not paste entire source files. Excerpt only what is needed to make the point.

## 7. Diagrams (Mermaid)

- Each `##` section with meaningful structural/relational/sequential content should have at least one diagram. Short prose-only sections are fine without.
- Diagrams must add structure the prose doesn't already provide. A diagram that restates a bullet list in boxes is noise.
- Choose the type deliberately:
  - Flow and branching → `flowchart`
  - Interaction across actors over time → `sequenceDiagram`
  - Type/interface/class relationships → `classDiagram`
  - Lifecycle/state machine → `stateDiagram-v2`
  - Timeline/budget visualization → `gantt`
- Give each diagram a `### Figure X.Y.Z <title>` heading so other pages can cross-link to it.
- For `classDiagram`, note: `A <|-- B` means *B inherits from A*; `A <|.. B` (or `B ..|> A`) means *B realizes A*. Don't mix these up when drawing interface relationships.

## 8. Cross-linking

- Within the same Part: relative path, no `.md` extension (the site uses `cleanUrls`).
  - `[1.1 Sampling](./01-sampling)`
- Across Parts: relative up-and-over.
  - `[4.11 Latency](../04-vst3-sdk/11-latency-tail)`
- External sources: full URL.

## 9. Terminology

<!-- FILL: project-specific terminology table. Example below. -->

| Term (canonical) | Alternate forms (do not use) | Definition / notes |
|------------------|------------------------------|--------------------|
| <term>           | <alt>                        | <brief definition> |

If a new term emerges during writing that isn't in this table, define it at first use and flag in your completion report that the glossary may need an update.

## 10. Frontmatter

Every page starts with:

```yaml
---
title: "<same wording as the H1>"
---
```

Titles containing `:` must be quoted — unquoted `title: Part 0: Intro` is invalid YAML.

## 11. Figure-number convention

Use `### Figure <Part>.<Chapter>.<Index> <short title>` for diagram headings so they're stable cross-reference targets. Example: `### Figure 2.4.1 PDC alignment before and after`.

From other pages, link as `[Figure 2.4.1](../02-.../04-chapter#figure-2-4-1-pdc-alignment-before-and-after)`. (VitePress anchor slugs are lowercased with hyphens.)

## 12. Prohibited

- Emojis.
- Subjective evaluations of tools, products, or people ("the best", "the most powerful", "superior to").
- Marketing language.
- Unverified claims without the `NOTE: unverified` marker.
- Editing files outside your assigned scope (in parallel-writing contexts).
- Running dev/build/deploy commands (reserved for the orchestrator).
