# /update-wiki

Push new findings from this OpenClaw development session into the research wiki at `../research-wiki/`.

## When to Use

Invoke `/update-wiki` after any development work that produces:
- A new finding about a prompt injection attack or defense
- A completed or failed experiment result
- An implementation decision with security implications
- A new concept that needs a formal definition

## Workflow

1. Read `git diff HEAD~1` (or the current conversation context) to understand what changed
2. Identify the correct wiki category: `attacks/`, `defenses/`, `experiments/`, or `concepts/`
3. Write or update the appropriate page in `../research-wiki/<category>/`
4. Update `../research-wiki/index.md` — add or update the entry for every changed page
5. Append to `../research-wiki/log.md`:
   ```
   ## [YYYY-MM-DD] update-wiki | <one-line summary of what changed>
   ```
6. Commit the wiki changes:
   ```bash
   cd ../research-wiki
   git add .
   git commit -m "wiki: <what was updated>"
   git push
   ```

## Behavior Rules

- No discussion phase — read context, write, commit
- If a finding is ambiguous (attack or defense), file it in the most specific category and cross-link from the other
- Flag speculation explicitly in the page body: **Note (unverified):** ...
- Always update both `index.md` and `log.md` — never skip these two files
- Keep entries factual and concise

## Page Templates

### Attack page (`attacks/<name>.md`)

```
# <Attack Name>

**Description:** ...
**Mechanism:** ...
**Example:** ...
**Severity:** low | medium | high | critical
**Affected surfaces in OpenClaw:** ...

## Sources
- [Source Title](../sources/YYYY-MM-DD-slug.md)

## Related Defenses
- [Defense Name](../defenses/defense-name.md)
```

### Defense page (`defenses/<name>.md`)

```
# <Defense Name>

**Mechanism:** ...
**Strengths:** ...
**Weaknesses:** ...
**Implementation complexity:** low | medium | high
**Status:** proposed | in-progress | tested | rejected

## Related Attacks
- [Attack Name](../attacks/attack-name.md)

## Sources
- [Source Title](../sources/YYYY-MM-DD-slug.md)

## Experiments
- [Experiment Name](../experiments/experiment-name.md)
```

### Experiment page (`experiments/<name>.md`)

```
# <Experiment Name>

**Hypothesis:** ...
**Method:** ...
**Setup:** ...
**Result:** ...
**Conclusion:** ...

## Attacks Under Test
- [Attack Name](../attacks/attack-name.md)

## Defenses Under Test
- [Defense Name](../defenses/defense-name.md)
```

### Concept page (`concepts/<name>.md`)

```
# <Concept Name>

<Definition paragraph.>

## Related Concepts
- [Concept Name](concept-name.md)
```

## Cross-Reference Format

From a category page (e.g., `attacks/`) to another category: `[Name](../defenses/name.md)`
From `index.md` at root: `[Name](attacks/name.md)`
