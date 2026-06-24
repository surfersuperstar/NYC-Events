# NYC Events Digest — build instructions (CI version)

You are compiling a twice-weekly digest of free and cheap events happening in NYC, with a focus on Williamsburg, Brooklyn. The digest covers evenings (weeknights after 5pm) and weekends. Cover the next 3–4 days from **today's date** (use the current date of this run; runs happen Tuesday & Friday mornning US-Eastern).

**CRITICAL EXTRACTION RULE: For every source you fetch, extract EVERY single event that fits the constraints — do not summarize, do not pick highlights, do not stop after a few. Newsletters and Substack posts often list 20–50+ events. Your job is to capture all of them. The finished HTML digest should have 60–100+ events. If a source yields fewer than 5 events, you likely missed content — re-read it carefully.**

> This file is the source of truth for the recurring GitHub Actions run. The surrounding workflow handles publishing (git commit/push) and the email — see STEP 7. Your job is ONLY to gather events and write `index.html`.

---

## STEP 1 — Fetch these sources directly (confirmed working URLs)

1. **The Skint** — https://www.theskint.com
2. **NYC for FREE** — https://www.nycforfree.co/events
3. **Club Free Time** — https://www.clubfreetime.com/new-york-city-nyc/free-events-things-to-do/this-weekend (use /this-weekend — more reliably current than /this-week)
4. **Blankman List** — https://www.blankmanlist.com/p/free-highlights-things-to-do-in-nyc-[month]-[year]
5. **Time Out NY** — Search `site:timeout.com/newyork "things to do in new york this week" [current date]` to find the current week's article URL, then fetch it. The rolling URL /things-to-do-in-new-york-this-week often shows the previous week — always get the current one via search first.
6. **Brooklyn Brainery** — https://brooklynbrainery.com/courses/prospect-heights (include only $20 or under)
7. **NYPL Events** — https://www.nypl.org/events/calendar (shows today's events). Also search `nypl.org events free [current date range]` to find events on other days this week.
8. **Lincoln Center Atrium** — https://www.lincolncenter.org/venue/atrium/v/calendar (always free)
9. **Lincoln Center Free series** — https://www.lincolncenter.org/series/lincoln-center-presents/v/calendar/s/Free
10. **MoMA PS1** — https://www.momaps1.org/en/calendar (free admission since Jan 1, 2026)
11. **Brooklyn Botanic Garden** — https://www.bbg.org/visit/calendar (note garden admission; flag accordingly)
12. **GrowNYC** — https://grownyc.org/events (in-person events only)

---

## STEP 2 — Substacks: search for latest post URL then fetch

**SSL NOTE**: Some Substack domains return intermittent SSL certificate errors. If direct fetch fails with SSL/cert error, extract event details from the search result snippets instead — do not skip the source entirely.

- **No Sleep Club NYC**: search `nosleepclubnyc.substack.com things to do this week [current month year]` → fetch top result. Always fully public with 40–50+ events — extract ALL of them.
- **City Happenings**: search `cityhappenings.substack.com nyc happenings events [current month year]` → fetch (URL format: /p/nyc-happenings-and-events-[month]-[day])
- **Marked (Morgan McDonald)**: search `markedbymorgan.substack.com this week nyc [current month year]` → fetch (URL format: /p/this-week-in-nyc-marked-[slug]). If SSL error, use snippet content.
- **warmly (calli)**: search `callikayferg.substack.com nyc this week goods [current month year]` → fetch. Paywalled after ~2 events; include free preview only.
- **Cool Stuff NYC**: fetch https://coolstuffnyc.substack.com/archive → find most recent post URL → fetch that post
- **Next Stop: IRL**: search `thevisioncatalyst.substack.com nyc events [current month year]` → fetch (URL format: /p/next-stop-irl-nyc-events-and-beyond-[slug]). Focuses on networking/professional events — tag as networking category.
- **Alex Feim Art Map**: search `alexfeim.substack.com nyc art map recs [current month year]` → fetch. Weekly free gallery guide.
- **Field Notes NYC**: fetch https://fieldnotesnyc.substack.com/archive → find most recent "things to do in new york" post URL → fetch it. Free through Thursday's events; Friday–Sunday is paywalled — include only the free portion.
- **One Fine Day NYC**: search `onefinedaynyc.substack.com "nyc this week" [current month year]` → fetch top result (URL format: /p/nyc-this-week-[month]-[day]-[day2]). Fully free weekly roundup by Taylor Tonkinson — free events, markets, outdoor activities.
- **Bite The Apple (Katie Romero)**: paywalled — skip, note in footer
- **The Underground**: SF-focused — skip, note in footer

---

## STEP 3 — GM NYC

1. Fetch https://www.gmnyc.com/archive
2. Find the most recent gmnyc.com/p/gm-nyc-[slug] URL and fetch it
3. Include: social events, parties, music nights, club nights, runs (e.g. Pitch & Run), concerts
4. Skip: pure enterprise/SaaS conferences, invite-only founder dinners with no public access

---

## STEP 4 — Search-based sources

- **NYC Parks**: search `site:nycgovparks.org/events free brooklyn [current date range]` — extract from snippets only (individual pages 403)
- **Urban Park Rangers**: search `site:nycgovparks.org/events/urbanparkrangers [current month year]` — extract from snippets
- **Do NYC**: Try fetching `https://donyc.com/events/[year]/[month]/[day]` for each day of the week (e.g. donyc.com/events/2026/05/4). If that returns SSL/403 errors, search `site:donyc.com free events Brooklyn Williamsburg [current date range]` and extract from snippets. Also search `site:donyc.com freewilliamsburg [current month year]` for Williamsburg-specific free events.
- **Secret NYC**: search `secretnyc.co free events NYC this week [current month year]`
- **Luma**: search `luma.com free events NYC Brooklyn Williamsburg [current month year]`
- **Resident Advisor**: search `ra.co free cheap events NYC Brooklyn [current month year]`
- **Meetup (general)**: search `meetup.com free events NYC Williamsburg Brooklyn this week [current month year]`
- **Meetup (business/tech/social)**: search `meetup.com free business networking tech learning social NYC [current month year]`
- **Dice.fm**: search `dice.fm free cheap shows brooklyn williamsburg [current month year]`
- **Eventbrite**: search `eventbrite.com free events brooklyn williamsburg this week [current month year]`
- **Bandsintown / Songkick**: search `bandsintown.com OR songkick.com free shows brooklyn nyc this week [current month year]`
- **Fever NYC**: search `feverup.com new york free cheap events [current month year]`
- **Creative Mornings Brooklyn**: search `creativemornings.com brooklyn [current month year]`
- **Secret Science Club**: search `secretscienceclub.net events [current month year]`
- **Jane's Walk NYC** (May only): search `mas.org janes walk nyc [current year]`
- **Museum free nights**: search for Whitney Free Fridays, MoMA Free Fridays, Brooklyn Museum First Saturdays for specific dates this week

**Permanently inaccessible — note in footer only:**
- Nonsense NYC — email only
- Found NY — paywalled (ny.itsfound.com)

---

## STEP 5 — Deduplicate across sources

Before tagging, merge any events that appear in multiple sources (same event name + same date):
- Keep the most complete description
- Set `source` to a combined string, e.g. `"The Skint / Time Out NY"`
- Set `sourceUrl` to the most specific URL available
- Do NOT produce two separate event objects for the same event

---

## STEP 6 — Tag every event

- **category**: music, comedy, art, markets, runs, film, talks, outdoors, food, learning, networking, wellness, other
- **days**: array, e.g. ["fri","sat"]. Events spanning 4+ days get all applicable days.
- **williamsburg**: true if venue is in or very near Williamsburg, Brooklyn

---

## STEP 7 — Generate `index.html` (NO publishing, NO email)

Generate the full self-contained HTML and write it to **`index.html` in the repository root**.

- The existing `index.html` is the PREVIOUS edition — read it if useful as a layout reference, but you are replacing it with a fresh edition for the new date range.
- **Overwrite safely:** the Write tool refuses to overwrite a file you have not read. The simplest reliable approach is to first delete it from the shell (`rm -f index.html`) and then write the new file. (Alternatively, read it first, then write.)
- **Do NOT run git / commit / push.** The GitHub Actions workflow commits and publishes `index.html` to GitHub Pages.
- **Do NOT send any email.** The workflow sends the notification email after publishing.

Self-contained HTML (inline CSS + JS, only Google Fonts CDN external).

### Header
Title + date range, subtitle, updated date. "↺ Update" button: calls `window.location.href='claude-digest://update'` then shows toast: "Launching updater… a terminal window will open and refresh the digest (5–10 min). Then reload this page."

### Filters (sticky, 4 rows, AND logic)
- Row 1: Search + live count + ✕ + "Clear filters"
- Row 2: Day chips
- Row 3: Category chips (All | Music | Comedy | Art | Markets | Runs | Film | Talks | Outdoors | Food | Learning | Networking | Wellness | Other)
- Row 4: Source chips (dynamically generated from events array, alphabetical)

### Williamsburg strip
Horizontal scroll strip of williamsburg=true events, always visible, respects filters.

### Museum Free Nights box
Always visible (Whitney, MoMA, Brooklyn Museum, Met).

### Main events grid — grouped by day with headers
Group events into day sections. Each section:
- Day header: day name (e.g. "Friday") · date (e.g. "Apr 17") · event count badge
- Responsive card grid (3-col desktop / 2-col tablet / 1-col mobile)

Events with days.length >= 4 go in a separate **"Ongoing"** section at the bottom (after all day sections), with an accent-colored header.

CSS structure: .day-section > .day-header (.dh-name, .dh-date, .dh-count) + .day-grid
Ongoing: .day-header.ongoing with accent color on .dh-name

### Event cards
name (bold), date+time (muted), venue+neighborhood, price badge (green=Free/yellow=$1–10/blue=$11–20), one-sentence desc, source linked text, ★ Wburg gold badge if williamsburg=true, category chip

Category colors: music:#a855f7 · comedy:#f97316 · art:#ec4899 · markets:#14b8a6 · runs:#22c55e · film:#ef4444 · talks:#3b82f6 · outdoors:#84cc16 · food:#f59e0b · learning:#06b6d4 · networking:#8b5cf6 · wellness:#10b981 · other:#64748b

### NBR Runs table
Always visible at bottom. Calculate which Friday of month; highlight applicable Friday runs green.

Runs: Mon Morning Easy 6:45am · Mon Night Easy 7:30pm · Wed Beginner 7pm · Wed Night Road 7:30pm · 1st Fri Salmon Run 7:30am · 2nd Fri Donut Run 7:30am · 2nd Fri Brewery Run 6:30pm · 3rd Fri Ice Cream Run 6pm · 4th Fri Bagel Run 7:30am · Sat Bridge & Coffee 9am · Sat Long Run (Narwhals) 7am · Sun Funday Long Run 8:30am

### Footer
List inaccessible/paywalled sources. Standing note: "Instagram accounts worth checking manually: @thekatieromero · @celinaprentiss · @nyc_forfree · @secretnyc · @nonsensenyc"

For reliability with a large number of events, you may write a small Python generator script in /tmp that takes an events JSON array and emits the HTML, rather than hand-writing the whole file — but the final artifact must be `index.html` in the repo root, fully self-contained, and validated (events JSON parses, no duplicate name+date pairs, all category/day-code values valid).

---

## Constraints
- Free or under ~$20 only
- Prioritize evenings (after 5pm weekdays) and all-day weekend events
- Do NOT include events whose date has already passed (before today)
- Do NOT fabricate events
- HTML must be fully self-contained
