# Key populations-sensitive health services and programming

> ## PILOT VERSION
>
> This is a pilot for internal testing. Content, references and features are still
> under review. **This is not the final version.** Do not cite it or circulate it
> outside the review group.
>
> To test it, work through **[TESTING.md](TESTING.md)**, which lists every interactive
> feature, what to expect, and the gaps that are already known.

An interactive planning, implementation and monitoring tool bringing together WHO
guidance on key populations-sensitive health services and programming. It enables
countries and partners to explore recommended interventions, assess reported service
availability, identify gaps and support the adaptation of global guidance to national
and local contexts.

The tool provides a rapid planning assessment. It does not replace comprehensive
programme review, consultation with communities, national policy processes or
context-specific technical guidance.

## Publishing on GitHub Pages

1. Push the contents of this folder to the default branch.
2. **Settings → Pages**, set **Source** to *Deploy from a branch*, choose your branch
   and the `/ (root)` folder.
3. The site is served at `https://<owner>.github.io/<repository>/`.

`.nojekyll` must stay in place. A GitHub Actions workflow is provided as an
alternative in `.github/workflows/pages.yml` — use one method or the other.

## Contents

| Path | What it is |
| --- | --- |
| `index.html` | The complete tool. No build step, no runtime dependencies. |
| `404.html` | Not-found page pointing back to the tool. |
| `assets/downloads/` | Source copy of the checklist. See MAINTENANCE.md. |
| `.nojekyll` | Disables Jekyll processing. |
| `LICENSE` | **Placeholder — must be set before publishing.** |
| `MAINTENANCE.md` | How to update content, references and the checklist. |
| `TESTING.md` | Step-by-step functionality test guide for the pilot. |

## Before public release

These remain outstanding and cannot be closed from inside the code:

- **Set the licence.** See `LICENSE`.
- **Test every link from the deployed URL** in Safari, Chrome and Firefox. Automated
  checks from a sandbox return 403 from who.int and iris.who.int regardless of
  whether the document exists, so they prove nothing.
- **Test the generated reports** in desktop Word, mobile Word, LibreOffice and Google
  Docs. They are Word-compatible HTML with a `.doc` extension, not Open XML.
- **Test with a keyboard and a screen reader.** ARIA roles and states are in place and
  were checked by simulation, but no assistive technology has actually been used.
- **Run a colour contrast audit** across the five population palettes.
- **Have the technical unit review the reference corrections** made during editing,
  and the wording of the methodological note in the Essential package tab.
- **Confirm the AI attribution statement** in the footer is accurate and sufficient.

## Known limitations

- Population-specific indicators exist for no population: the earlier TGD and PWID
  sections were removed when indicators were restricted to GAM and WHO sources.
- The overlap pages are written and reachable from the cross-cutting summary, but the
  diagram has no clickable intersection labels.
- The "Resources" and "Abbreviations" tabs have supporting code but no content.
- Assessment answers survive navigation within a session but are not saved to the
  device. Persisting them would need `localStorage`, a privacy notice and a delete
  control — see MAINTENANCE.md.

## Long-term structure

The tool is deliberately a single self-contained file so that it works offline and can
be shared by email or memory stick. That choice has a cost: content, code and styling
live together, which makes review, translation and a strict Content Security Policy
harder.

If the tool moves to a maintained product, the content should be lifted out into
`assets/data/*.json` (populations, interventions, indicators, publications,
references) with the code in `assets/js/`, and the page assembled at build time. That
would keep the single-file output while making the substance reviewable on its own.
This has not been done: it is a rewrite, not an edit, and it should be planned rather
than improvised.
