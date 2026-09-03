# Maintenance notes

`index.html` is a single self-contained file. There is no build step: edit the file
and commit. The notes below cover the parts that are not obvious from reading it.

## The downloadable checklist is embedded twice over

The Word checklist exists in two places:

- `assets/downloads/WHO_key_populations_interventions_checklist.docx` — the source file.
- Inside `index.html`, base64-encoded in the JavaScript constant `CHECKLIST_DOCX`.

The download button reads the constant, not the file in `assets/`. Embedding it
this way is what allows the tool to work offline and as a single shared file, but it
means **updating the docx in `assets/` alone has no effect on what users download.**

To update the checklist:

```bash
# 1. Replace the source file
cp new_checklist.docx assets/downloads/WHO_key_populations_interventions_checklist.docx

# 2. Re-encode and substitute the constant in index.html
python3 - <<'EOF'
import base64, io, re
b64 = base64.b64encode(
    open("assets/downloads/WHO_key_populations_interventions_checklist.docx", "rb").read()
).decode()
s = io.open("index.html", encoding="utf-8").read()
s = re.sub(r'var CHECKLIST_DOCX = "[A-Za-z0-9+/=]*";',
           'var CHECKLIST_DOCX = "%s";' % b64, s, count=1)
io.open("index.html", "w", encoding="utf-8").write(s)
EOF

# 3. Verify the round trip before committing
python3 - <<'EOF'
import base64, hashlib, io, re
s = io.open("index.html", encoding="utf-8").read()
d = base64.b64decode(re.search(r'var CHECKLIST_DOCX = "([A-Za-z0-9+/=]+)";', s).group(1))
o = open("assets/downloads/WHO_key_populations_interventions_checklist.docx", "rb").read()
print("identical:", hashlib.sha256(d).hexdigest() == hashlib.sha256(o).hexdigest())
EOF
```

The download button appears only on the **Essential package** tab, in each of the
five population pages and in the cross-cutting summary. Six buttons, one shared
constant.

## References

There are 64 numbered references. Each population has its own copy of the list in
`D.<POP>.refs`, and **entry 3 differs by population** — it is that population's own
recommended package policy brief. Everything else is identical across the five.

Three invariants are worth checking after any edit to references or citations:

1. **Every inline citation's `href` matches the URL of that number in that
   population's list.** A citation numbered 3 on the sex workers page must link to
   the sex workers policy brief, not the one for men who have sex with men.
2. **Every reference is cited at least once**, and every cited number exists.
3. **The "Page references" box at the foot of each intervention tab lists exactly
   the numbers cited on that tab.** These are not generated at runtime; they are
   static and must be regenerated when citations change.

Each citation also carries a `title` attribute holding the full reference text, so
that hovering shows the source rather than a bare URL. The number inside the
`title` must match the number displayed in the link.

Every reference also appears in the WHO publications tables inside the tool. The
tables hold more entries than the reference list — additional publications are
offered there as supporting reading without being cited.

## Diagram behaviour

Clicking a population circle focuses it; clicking the same circle again, or the
empty space, returns to the combined image.

Focusing moves the selected circle to the end of its SVG parent so that it draws
in front. `unselectAll()` restores the original stacking order, but only after a
580 ms timer, so that the circle does not jump behind the others while it is still
animating back. **That timer is tied to the 0.55 s CSS transition on `.kp-unit`.**
If you change the transition duration, change the timer too, or the stacking order
will snap back early.

## Section labels are load-bearing

The checklist gap summary classifies findings by matching the text of section
headings — `"Enabling interventions"`, `"Health interventions"`,
`"Broader health"`, `"Supportive"`. Renaming a tab heading without updating those
string comparisons silently empties the gap summary.

## Content that is known to be incomplete

- The overlap pages (`D.<POP>.overlaps`) are written and reachable from the
  cross-cutting summary, but the SVG has no clickable intersection labels, so
  `showOv()` is never called from the diagram itself.
- The "Resources" and "Abbreviations" tabs have supporting code (`filterRes()`,
  the `.res-*` styles) but no content and no tab buttons.
- The interactive checklist functions expect `.cl-item`, `.cl-box` and `.cl-group`
  classes that no current content emits.
- Population-specific indicators exist for trans and gender diverse people and for
  people who inject drugs, but not for the other three populations.


## Escape levels: the trap that bites hardest

Content lives inside JavaScript strings at two different nesting depths:

- `D.<POP>.<tab>` strings use `\"` for attribute quotes.
- `crossCuttingSummaries` and `OV` are nested one level deeper and use `\\"`.

Using the wrong one produces `class=""kp-lbl""`, which the browser reads as an empty
attribute. The markup looks right in the source and silently loses all styling in the
browser. This has already happened twice. **Always check `grep -c '=\\"\\"' index.html`
returns 0 after editing content strings.**

## Assessment state

Answers are held in `assessmentState`, keyed by population and by the label text of
each item, and restored after every `render()`. Nothing is written to the device.

To persist between sessions, serialise `assessmentState` to `localStorage` under a
versioned key, and add both a privacy notice and a "Delete saved assessment" control.
`kpClearAssessment()` already exists as the clearing function.

## Accessibility layer

Keyboard and screen-reader support is added by `kpSyncAria()`, which applies
`role`, `aria-checked`, `aria-selected` and `aria-pressed` to elements that are not
native controls. It must be called after anything that rebuilds or mutates the panel.

This is a layer over non-native markup, not a native solution. Converting the
checklist items to real `<input type="checkbox">` and the diagram circles to real
`<button>` elements remains the proper fix.
