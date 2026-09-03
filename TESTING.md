# Functionality test guide — pilot

Walk this list in a browser and record what you see. It covers every interactive
feature that is actually wired up in the page, plus the features that exist in the
code but have no way to reach them.

Test on at least: one desktop browser, one phone, and once using only the keyboard.

Record the browser, the device and the date at the top of your notes. Where something
fails, note the exact steps, because most of these depend on the order of actions.

---

## 1. Diagram

| # | Action | Expected |
| --- | --- | --- |
| 1.1 | Click a population circle | It stays full size and opaque; the other four shrink and move outward; the tab panel opens for that population |
| 1.2 | Look at the four shrunken circles | Their labels and icons stay legible, sit outside the circle, and keep an even gap from it |
| 1.3 | Click the same circle again | Everything returns to the combined image, smoothly, with the original overlap order |
| 1.4 | Click the empty space inside the diagram | Same return to the combined image |
| 1.5 | Click somewhere else on the page (white space, a paragraph) | **Nothing should happen.** The selection must survive |
| 1.6 | Select a circle, then select a different one directly | The first returns to size while the second grows; no flicker in the stacking order |
| 1.7 | Read the hint line under the diagram | One sentence only, and it changes when a population is selected |

## 2. Diagram by keyboard

The button row that used to sit below the diagram has been removed. The circles
themselves are now the only population control, so keyboard access depends on them.

| # | Action | Expected |
| --- | --- | --- |
| 2.1 | Press Tab repeatedly from the top of the page | Focus reaches each of the five circles in turn, with a visible outline |
| 2.2 | With a circle focused, press Enter | That population is selected |
| 2.3 | With a circle focused, press Space | Same, and the page must not scroll |
| 2.4 | Use a screen reader on a focused circle | It is announced by the population name, as a button, with its pressed state |

## 3. Tabs

| # | Action | Expected |
| --- | --- | --- |
| 3.1 | Click each of the ten tabs | The panel content changes; the active tab is visibly marked |
| 3.2 | Click the active tab again | The panel returns to the "Select a tab" message |
| 3.3 | On a phone, look at the tab rail | It scrolls sideways; a fade appears on the right edge; the hint "Swipe sideways for more sections" is visible |
| 3.4 | Focus a tab and press Left and Right arrows | Focus moves between tabs and the content follows |
| 3.5 | Press Home and End while on a tab | Jumps to the first and last tab |

## 4. Address bar and browser navigation

| # | Action | Expected |
| --- | --- | --- |
| 4.1 | Select a population and a tab, look at the address bar | It shows something like `#population=pwid&section=supportive` |
| 4.2 | Copy that address into a new tab | The page opens on the same population and section |
| 4.3 | Press the browser Back button | Returns to the previous view |
| 4.4 | Open `index.html` directly from disk (file://) | The page still loads and works; the address may not update, which is expected |

## 5. Expandable sections

| # | Action | Expected |
| --- | --- | --- |
| 5.1 | Open a section in Essential package | It expands; the title stays visible and correctly styled |
| 5.2 | Open a second section, on any screen size | The first closes: only one section is open at a time |
| 5.4 | Click "Expand all" then "Collapse all" | All sections in the panel open and close together |
| 5.5 | Check the sub-sections under Health interventions | Prevention, Testing and diagnosis, Treatment and care are nested inside |

## 6. Statement type labels

| # | Action | Expected |
| --- | --- | --- |
| 6.1 | Open Enabling, Health, Broader health and Supportive | Every statement carries a coloured label: WHO recommendation, WHO conditional recommendation, WHO good practice statement, WHO guidance statement, or Summary |
| 6.2 | Compare the colours | The five are distinguishable, and the text alone still tells you which is which |

## 7. References

| # | Action | Expected |
| --- | --- | --- |
| 7.1 | Hover a numbered citation in the text | A tooltip shows the full reference, not the URL |
| 7.2 | Click a numbered citation | The publication opens in a new tab |
| 7.3 | Open any intervention tab and find the "Page references" box | Every `[n]` is a link |
| 7.4 | Click one | You land on the References tab, scrolled to that entry, which is briefly highlighted |
| 7.5 | Click "Back to content" | You return to the tab you came from |
| 7.6 | Check the numbering | It runs 1 to 67 with 46, 47 and 50 absent: those three community engagement publications now live only in the WHO Publications tab |

## 8. WHO Publications tab

| # | Action | Expected |
| --- | --- | --- |
| 8.1 | Open the tab | Twelve covers appear immediately under "Key population guidelines and policy briefs", without needing to expand anything |
| 8.2 | Scroll the cover strip sideways | All twelve are reachable; each has a Vancouver citation underneath |
| 8.3 | Click a cover | The publication opens in a new tab |
| 8.4 | Click "All publications in this section (table)" | The table expands |
| 8.5 | Switch population | The covers and the tables stay the same for every population |

## 9. Intersecting needs tab

| # | Action | Expected |
| --- | --- | --- |
| 9.1 | Look at the five rows | Each has a checkbox, a population icon, and a label, all on one line and vertically centred |
| 9.2 | Narrow the window until a label wraps to two lines | The checkbox and icon stay centred against the two lines |
| 9.3 | Tick two populations | The service list on the right updates |
| 9.4 | Click "Clear all" | All rows clear |
| 9.5 | Tab to a row and press Space | It toggles |

## 10. Downloads

Reports and pages are now produced as PDF through the browser's print dialog, so the
output cannot be edited. The checklist template stays a Word file because it is meant
to be filled in.

| # | Action | Expected |
| --- | --- | --- |
| 10.1 | Click "Download as PDF" on any tab | A new tab opens with a print-formatted version and the print dialog appears |
| 10.2 | Choose "Save as PDF" as the destination | A PDF is saved; a confirmation appears on the original page |
| 10.3 | Open the PDF | A4 pages, readable tables, no buttons or expand arrows, links still clickable |
| 10.4 | Check the top of the PDF | It carries the pilot notice and the generation date |
| 10.5 | Check that all sections appear | Collapsed sections are expanded in the PDF, not omitted |
| 10.6 | Block pop-ups for the page, then try again | A message tells you to allow pop-ups; nothing fails silently |
| 10.7 | Click "Download checklist as Word" in Essential package | A `.docx` downloads with a confirmation |
| 10.8 | Open it in Word on desktop and on a phone | It opens without a format warning |
| 10.9 | Try on a phone | Note whether the print-to-PDF flow works on iOS and Android, which is the least predictable part |

## 11. Indicators tab

| # | Action | Expected |
| --- | --- | --- |
| 11.1 | Open the tab for each population | Only indicators sourced GAM or WHO appear |
| 11.2 | Count the sections | Prevention cascade, Testing and diagnosis, Treatment and viral suppression, Structural and enabling |
| 11.3 | Check the intro paragraph | It cites four sources, each with its own number |

## 12. Accessibility

| # | Action | Expected |
| --- | --- | --- |
| 12.1 | Navigate the whole page using only Tab and Shift+Tab | Every control is reachable and shows a clear blue focus outline |
| 12.2 | Check the diagram | The SVG itself is skipped; the population buttons below are the way in |
| 12.3 | Turn on "reduce motion" in your operating system, reload, select a circle | The change happens instantly, without animation, and nothing disappears |
| 12.4 | Use a screen reader on the tabs | They are announced as tabs, with the selected one identified |
| 12.5 | On a phone, try to tap the small controls | Every target is comfortable to hit |

## 13. Text and terminology

| # | Action | Expected |
| --- | --- | --- |
| 13.1 | Search the page for "Transgender and gender-diverse" | No results; the approved form is "Trans and gender diverse people" |
| 13.2 | Search for "prisons and closed settings" | No results; the approved form includes "other" |
| 13.3 | Read the pilot banner and the homepage definition | Both present and accurate |
| 13.4 | Open Essential package | The scope qualification and the "Before you begin" note are both there |

---

## Known gaps — do not report these as new

These are already identified. Test around them.

**The interactive checklist does not exist.** The page has no tickable service items.
The classes the code looks for are never emitted by any content. As a result these
functions cannot be reached from the interface at all:

`toggleCheck`, `clToggle`, `clExpand`, `resetChecklist`, `generateSummary`,
`downloadChecklistPage`, `kpClearAssessment`

The two report generators now produce PDF rather than Word, but they still cannot be
reached from the interface.

Recording answers is done in the downloadable Word checklist instead, which is what
the instructions now say.

**Other unreachable code:** `showOv` (the overlap pages exist but the diagram has no
clickable intersection labels), `filterRes` (the Resources tab has no content or tab
button), `insName`, `kpPush`.

**Not yet verified by anyone:** every external link from a deployed URL, the generated
reports in real Word, screen reader behaviour, and colour contrast.

---

## What to send back

For each numbered test: pass, fail, or not applicable. For failures, the browser, the
device, the exact steps, and a screenshot if the problem is visual. Group anything
that only happens on one device, because most of the layout work has been done by
reading the code rather than by looking at a screen.
