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
2. Clicks **Apply / Apply Now / Easy Apply** if needed to open the application form,
3. Runs **Jobright autofill**,
4. Fills any gaps + commits location/required fields,
5. **Submits and verifies the submission was confirmed** — retrying fill+submit if
   not — *before* moving to the next job. A job only counts as done once submission
   is confirmed; otherwise it's marked **failed** (not a false "applied").

The control panel stays open for the whole run (it mounts on every job page, including
listing pages), so you always see progress and can Pause / Skip / Quit / change Speed.

### Automation panel (matches 1.14.0)

While the queue runs, a panel shows in the top-right:

- **Automation In Progress** · **Job X of N**
- **Position at …** (current company) with a live progress bar
- **Pause / Skip / Quit**
- **Speed:** `1x` `1.5x` `2x` `3x` — controls the delay between jobs

Progress is saved per-job, so if a page reloads or you stop midway, **Resume**
continues from where it left off.

### Managing the queue

The sidebar card has a full queue manager: tick individual jobs or **All**, then
**Delete selected**, or **Clear all**. Each row shows the job and its live status,
with a **×** to remove it. Works on the whole queue even when large.

### ATS account login (saved credentials)

Some ATS (Workday, iCIMS, Taleo, SuccessFactors, ADP/BrassRing, Jobvite…) make you
create an account or sign in before applying. This is **fully automatic across all ATS** —
no manual effort:

- The automation detects sign-in / create-account pages on **every** platform, fills the
  saved credentials (email, password, confirm-password, consent), submits, and falls back
  to sign-in if the account already exists.
- A strong password is **auto-generated and saved the first time**, and the email comes
  from your profile — so it works with zero setup. You can still view/override them under
  **🔑 ATS account login** in the sidebar card.
- Personal job-board logins (LinkedIn/Indeed/Glassdoor/etc.) are never touched.

### Self-navigating to completion

Each application drives itself to a **confirmed submission** with no supervision: it opens
the Apply form, clears any account wall, autofills, then advances through every page —
multi-step forms, review/confirm screens — clicking Next/Continue/Submit on its own. This
is a **universal driver that runs for all ATS platforms**, on top of the platform-specific
flows. Only once submission is confirmed does the queue move to the next job.

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
