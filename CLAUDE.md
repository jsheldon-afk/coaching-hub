# Seated Coaching Hub

Sales certification and performance system for Seated AEs and BDRs. Formerly "Seated University"; repo formerly `M1-AE-BDR-Quiz`, now `jsheldon-afk/Coaching-Hub`.

Owner/admin: James Sheldon (jsheldon@seatedapp.io), Sales Enablement & Ops at Seated.

## What Seated is (for content context)
Restaurant technology and demand-generation platform connecting diners with restaurant partners via the Seated app, Bilt, and the Dinova corporate dining network. Standard take rate is **18%**.

## The framework
The hub combines three things, shown as a **Success Feedback Loop** (this replaced an older triangle graphic, so don't bring the triangle back):
- **Knowledge & Systems**: certification modules and quizzes
- **Metrics**: outcome standards
- **Execution**: daily effort and behaviors

Core message: **reps own their numbers and their plan to get there; the manager's job is to give them a coaching plan to get there.** The homepage rewrite partly covers this, and it may need more work.

### Rep status tiers (use exactly these names)
1. High Risk
2. Performance Improvement Needed
3. Seated Standard
4. Seated Gold Standard

### Ramp stages (tenure-based)
- M0–M2: AE/BDR
- M3–M6+: 25% → 50% → 75% → 100% AE

## Site structure
- 11+ Knowledge modules on Month 0 / Month 1 / Month 2 tracks, with deadlines driven by the month system.
- **Supplementary** section uses one-time due dates instead of the Month 0/1/2 deadlines.
- Module source links point to the live Google Slides/Docs so content stays current.

### Weekly check-in
- Reps self-report metrics. Salesforce exports aren't an option (see Constraints).
- Meetings are tracked as **self-scheduled vs. inbound**.
- Win rate is a rep-entered rolling 30-day figure.
- **Pipeline confirmation is required before a check-in can be submitted**, to reinforce ownership.
- Save Draft is supported.
- Timeframe filter for week-over-week views.
- Month-end recap: restaurants, points, and take rate vs. the 18% standard. It opens the **3rd Monday of the following month**.

### Manager flow
Managers can **Approve** or **Suggest update**. Suggested changes go back to the rep to confirm.

Managers: Gradie Oakes (goakes@), Kristen Garcia (kgarcia@), Taylor Rozencwaig (trozencwaig@), all @seatedapp.io. Seated email format is first initial + last name @seatedapp.io. Module approvers: Pat and Gradie.

## Backend
- **Google Apps Script** handles score collection, roster matching, deadline alerts, and recertification.
  - POST uses `no-cors`, so responses are opaque and can't be read. Use GET with query params when you need readable JSON back.
- **Google Sheets** holds scores, the roster, and raw data (`Raw_Opps`, `Checkins` tabs).
  - The Sheet must be owned by jsheldon@seatedapp.io, or the "Anyone within Seated" Apps Script deployment option won't appear.
- Recertification cycles anchor to the rep's **start date**, not their completion date, so cohorts share cycle boundaries.
- Overdue modules re-trigger reminders every 7 days. **These reminder emails are currently paused (Nov 2026).** Don't turn them back on without James.

## Security / hosting
Moving off public GitHub Pages: the site goes behind **Google sign-in restricted to seatedapp.io accounts**, and the repo becomes private.

## Constraints
- **Don't poll the Salesforce API directly.** The org's shared daily API limit is used up by Nooks and Salesloft. Manual report exports (Opportunity, Activity) don't count against it and are the reliable path. Real exports were used to validate the calculation logic.

## Design system
- Seated palette: **cream / gold / ink**
- Headings: **Fraunces** (serif). Body: **Inter**
- Keep it simple and readable: bigger fonts, fewer concepts per screen, plain direct language.
- Verify visually with **Playwright** against local HTML via `file://` URLs. There's no dev server.

## Quiz & module design rules
- Build content from the **actual live source materials** (Google Slides/Docs). Don't guess.
- Correct multiple-choice answers must **match the distractors in length and specificity**, so the answer isn't given away.
- For content with a natural sequence (daily schedule, call structure, objection steps), add a drag-and-drop **"put these in order"** reorder exercise alongside the multiple choice.
- One **"Submit module"** button grades every section at once. Don't do per-section submit.
- Scorecard criteria use Seated-specific language with clear pass/fail definitions. No generic or duplicate questions.

### Domain terms
ARP (objection handling), TIPS (discovery framework, mapped to SPIN), cold call standards, Pitch Olympics, CWs (closed-won), ROE (Rules of Engagement), CRM hygiene, Nooks / Salesloft / Salesforce, Bilt / Dinova.

## Open items / roadmap
- **Inconsistency:** Product Economics Calculator is tagged Month 1 in `schedule.html` but Month 2 in `apps-script.txt`. Needs reconciling.
- **"To Come" section** (planned modules): Rate Calculator, Performance Metrics Standards, Pipeline: Following Up, Discovery, Ramped Commissions.
- **Missing pieces:** rewards, MQL eligibility.
- **Next iteration idea:** AI reads check-ins and gives managers coaching recommendations.

## Working style
- James iterates a lot on messaging and often simplifies after a first, more complex pass. Expect revisions.
- For team presentations: concise talking points (why → framework → rhythm → live demo), not scripts.
