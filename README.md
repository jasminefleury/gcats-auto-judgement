# G-CATS Auto-Judgement

Judgement support for IMDS material compliance at TMMIN. Import the daily G-CATS Error Check Log,
let the rules engine work through each error, answer the few questions it cannot decide alone, and
record a final OK/NG with its full evidence trail.

**The engine recommends. A person decides.** Nothing is marked final until an Approver confirms it,
and every recommendation keeps the reference versions and the step-by-step reasoning behind it.

Runs entirely in the browser — the G-CATS data never leaves the machine it is opened on.

## Screens

| Screen | What it is for |
| --- | --- |
| **Overview** | Progress, what needs attention first, workload by route, suppliers with the most open cases |
| **Judgement Register** | Every case, with the evidence chain and the decision panel |
| **Daily G-CATS Update** | Import today's Error Check Log; answers and decisions already made are kept |
| **Auto-Judgement History** | Append-only log of every answer, approval, override and re-open |
| **Supplier Follow-up** | Open questions grouped per supplier |
| **Substance References** | CAS lookup: GADSL → TSZ0001G group → POPs / REACH XVII / REACH XIV |
| **Judgement Rules** | The Appendix II flows the engine follows |

Light and dark mode, and it follows your system setting until you pick one.

## Deploy on Vercel

1. Go to [vercel.com/new](https://vercel.com/new) and import `jasminefleury/gcats-auto-judgement`.
2. Framework preset: **Other**. Leave the build command empty. `vercel.json` already sets the output
   directory to `public` and adds the security headers.
3. Deploy. Every push to `main` redeploys automatically.

Because the data stays in the browser, the deployment is just static hosting — no server, no database.
Anyone who can open the URL can use the app, so **protect the deployment**: in Vercel, turn on
Deployment Protection (Settings → Deployment Protection) or keep it to your Vercel team.

### Run it locally

Open `public/index.html` in a browser. That is all — there is no build step.

## Daily workflow

1. Download today's G-CATS Error Check Log and save it as `.xlsx` (old `.xls` must be re-saved first).
2. **Daily G-CATS Update** → drop the file in → check the preview → *Commit to register*.
3. **Overview** → start with what needs attention.
4. **Judgement Register** → open a case, read the evidence chain, answer the engine's question.
   *Apply to identical cases* answers a whole group at once; any case that reaches a different
   result on its own data is split back out.
5. Set your role to **Approver** to confirm a final OK/NG. A comment is always required; overriding
   the engine, or deciding a case it could not judge, also requires a written justification.
6. Export: **Excel (Error Log format)** with the judged rows filled in, a **PDF summary**, or **CSV**.

Each row is matched by module ID, version, error type, component, material and CAS — never by the
daily "No." — so tomorrow's import refreshes the register without losing your work.

## Data and storage

Your work lives in the browser's local storage, per browser and per machine. Clearing site data
erases it, and colleagues do not see each other's work. Export regularly.

Reference data embedded in the app: GADSL 2026, TSZ0001G Rev.30 (Appendix 2), Appendix 3 POPs,
Appendix 4 REACH XVII, Appendix 5 REACH XIV, TSZ2900G mass tolerance, the Pb TOYOTA policy table
and the supplier code master.

> Most reference sets are still marked `EXTRACTED_PENDING_ADMIN_APPROVAL`, and the Pb policy table is
> a draft transcription awaiting verification. Until their owners sign them off, treat every
> recommendation as a suggestion to check, not an answer to trust.

This reference data is Toyota PROTECTED material. Keep this repository private.

## Repository

```
public/index.html    the whole app (engine, UI and reference data in one file)
public/styles.css    theme and layout, light + dark
vercel.json          output directory and security headers
```
