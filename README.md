# Jobright Autofill — v1.14.0 Full-Auto Edition (CSV Queue)

Unpacked Chrome extension (Manifest V3) built on the **official Jobright Autofill
1.14.0** patch (last updated 2026-06-18), with a fully-automated, zero-supervision
bulk-apply queue layered on top. The native Jobright **1.14.0 UI/UX is preserved** —
the only addition is a separate automation panel that matches its look.

## Folders

| Folder | What it is |
| --- | --- |
| `Download Jobright Autofill … Version 1.14.0 Last updated 2026-06-18` | **Use this one.** Newest patch + full automation + CSV queue. |
| `Download Jobright Autofill … VERSION 5 -WORKS - 09-05-26` | Previous build (1.9.0 base), kept for reference. |

## Install (Load unpacked)

1. Open `chrome://extensions`
2. Enable **Developer mode** (top-right)
3. Click **Load unpacked**
4. Select the `… Version 1.14.0 Last updated 2026-06-18` folder

## What's new in this build

- **Newest base** — official Jobright Autofill **1.14.0** (2026-06-18).
- **100% automated / no supervision** — the queue self-heals so it never stalls
  waiting for a human:
  - Robust **Google-Places / typeahead location committer** — types the city,
    waits for the suggestion dropdown and *selects* it, clearing the common
    "Please enter your location" error that used to block submission.
  - **Required-field guarantor sweep** before every submit — any still-empty
    required field (selects, location, phone, email, text, numbers) is filled with
    a best-guess or safe default so the form is always submittable.
- **CSV upload → auto-apply queue** (LazyApply-style) — see below.
- **Native 1.14.0 UI/UX preserved** — no restyling of Jobright's own sidebar; only
  upgrade/paywall chrome is hidden so upsell modals can't interrupt the run.

## Upload a CSV and auto-apply

The bulk-apply controls live **inside the native Jobright sidebar** (under the
Autofill buttons) — no separate popup window. Open Jobright on any job/ATS page and
you'll see the **⚡ Bulk Auto-Apply** card. Then:

1. **Upload CSV** (`.csv` / `.txt` / `.tsv`) **or** click **Paste URLs** and paste a
   list (one job URL per line / comma / tab separated).
   - CSV format: one job URL per row. A header row (`url`, `link`, `job`, …) is
     auto-skipped. Extra columns (title, company, status) are ignored.
2. (Optional) tick **Tailor resume for each job** — off by default for speed and
   reliability (see note below).
3. Click **Start Applying**.

The queue then, for each imported URL:

1. Navigates to the job page,
2. Runs **Jobright autofill** (tailor → autofill),
3. Fills any gaps + commits location/required fields,
4. **Submits**, and moves to the next job automatically.

### Automation panel (matches 1.14.0)

While the queue runs, a panel shows in the top-right:

- **Automation In Progress** · **Job X of N**
- **Position at …** (current company) with a live progress bar
- **Pause / Skip / Quit**
- **Speed:** `1x` `1.5x` `2x` `3x` — controls the delay between jobs

Progress is saved per-job, so if a page reloads or you stop midway, **Resume**
continues from where it left off.

### Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| `Alt+S` | Start / stop the queue |
| `Alt+P` | Pause / resume |
| `Alt+J` | Add the current page to the queue |
| `Alt+F` | Run a manual fill pass on the current page |

## Notes

- Supports 150+ ATS platforms (Workday, Greenhouse, Lever, SmartRecruiters, iCIMS,
  Ashby, Workable, LinkedIn/Indeed Easy Apply, and more) plus multi-page forms.
- Each job has a 90s timeout — if a page stalls it auto-skips so the queue keeps moving.
- Review your profile in Jobright's **Your Autofill Information** before a large run so
  the autofill values (name, phone, **city**, work authorization, etc.) are correct.
- **Reliability:** the queue uses the plain **Autofill** path by default. The
  "Generate Custom Resume + Autofill" combo depends on Jobright's resume generator and
  can hang on *"Opening resume generator…"*, so it isn't used automatically unless you
  tick **Tailor resume for each job**. The credit/quota unlock no longer touches
  resume/cover-letter endpoints, so the generator's own responses aren't altered.
- An optional advanced panel (profile editor, saved responses, application history) is
  still available via the floating button, but it's no longer required for bulk applying.
