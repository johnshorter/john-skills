# Per-call grant guidelines

Drop one file per funding call in this folder. When the grant-writing skill runs, it looks
here first, reads the file that matches the call, and turns it into the reminder checklist it
shows before drafting. This is how each application's rules get surfaced automatically instead
of being rediscovered every time.

## Naming

`<funder>-<scheme>-<year>.md`, dash-case. Examples:

- `nnf-data-science-ascending-investigator-2026.md`
- `dff-research-project-1-2026.md`
- `ruc-proof-of-concept-2026.md`

## Template

Copy this into a new file and fill it in from the call text.

```md
# <Funder>: <Scheme> <Year>

- Deadline:
- Eligibility:
- Total budget / duration:
- Character or page limit, overall:

## Required sections, in order
1. <section> (limit)
2. <section> (limit)
...

## Evaluation criteria and weights
- <criterion> (weight)
- <criterion> (weight)
...

## Budget rules
- Eligible costs:
- Ineligible costs:
- Overhead / indirect cost rule:

## Formatting
- Font / margins / line spacing:
- Figures, references, CV format:

## Notes
- Anything idiosyncratic about this funder or call.
```

Keep these accurate and update them when a call changes year to year. An out-of-date guidelines
file is worse than none, because it produces a confident but wrong checklist.
