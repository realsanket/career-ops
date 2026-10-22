# Anchor your Finnish job search on career-ops

**Keep career-ops as your only core repo.** Every credible alternative on GitHub was checked on 2026-10-22, and none beats it for a cloud-only Claude workflow. None of them adds what you actually lack either. Your gaps are Finnish job sources and storage that survives between sessions, not features. The only full-featured rival, ai-job-search (63k stars), is a near-twin built Denmark-first, and it needs a heavier LaTeX, Bun and Python setup on every fresh cloud machine. The auto-appliers need a local Chrome and break LinkedIn's terms, and the rest each cover one stage that career-ops already handles. The final stack has four parts:

| Part | Role |
|---|---|
| Your public fork of career-ops | Code only. Nothing personal is ever committed to it |
| A new **private** GitHub data repo | Holds your CV, profile, tracker and reports, through career-ops' supported data-root override |
| Gmail job alerts | Cover the Finnish boards that forbid scraping |
| The Enhancv API | An optional second renderer and a way to import a CV. It is not part of the core pipeline |

In this setup Claude can find roles on the job-application systems (ATSs) that Finnish employers actually use, score fit, tailor fact-checked A4 CVs and cover letters, keep the tracker, draft follow-ups, run interview prep, and explain salary and permit thresholds. It cannot submit applications or even fill in application forms. It cannot legally read Duunitori or Työmarkkinatori, and it cannot reach the 70–80% of Finnish jobs that are never advertised. It also forgets everything you don't push to GitHub before a session ends. The market is weak, with trend unemployment at **10.1% in August 2026** ([Statistics Finland](https://stat.fi/en/publication/cmfp96le0a4mm07vyv0oyqv4n)), so the plan below favours a few strong applications plus networking over volume. Start today by creating the private data repo and proving that one save and reload works between two sessions. Start onboarding only after that passes.

## Only one rival matches career-ops, and it is built for Denmark

Two projects lead the "AI job search inside Claude Code" category. Both are MIT-licensed and get commits daily. **career-ops** has 76,475 stars and 14,177 forks, about 2,200 commits in the last 13 weeks, and a minor release roughly every 5–6 days ([career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops)). **ai-job-search** has 63,165 stars and its own daily commits ([ai-job-search](https://github.com/ai-job-search-dev/ai-job-search)).

The two work the same way. ai-job-search also scores fit, drafts a LaTeX CV and cover letter checked by a reviewer agent, preps interviews, tracks applications and never submits. Where they differ is the part that matters for you. ai-job-search finds jobs on Danish boards (Jobindex, Jobnet, Akademikernes Jobbank), on LinkedIn's guest endpoints and on freehire.me. It never mentions Finland, and it needs Python 3.10+, Bun and a LaTeX distribution ([ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search)), which every ephemeral cloud machine would have to install again. career-ops instead reads the ATS platforms Finnish employers use (Greenhouse, Ashby, Teamtailor, Workday, SuccessFactors, Oracle, SmartRecruiters, Workable), plus The Hub's Nordic startup feed ([SUPPORTED_JOB_BOARDS.md](https://github.com/career-ops-hq/career-ops/blob/main/docs/SUPPORTED_JOB_BOARDS.md)). It also has the strictest anti-fabrication design found: "Keywords get reformulated, never fabricated", plus scripts that check generated CVs against `cv.md` ([AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md)).

ai-job-search has two features worth envying: its `/add-portal` generator and its Gmail-sync approval flow. Neither justifies switching. career-ops already documents how to add a provider and has a `discover` mode, and your Gmail connector covers reply intake.

Every other candidate either covers one stage or fails in the cloud:

| Repo (verified 2026-10-22) | What it is | Fit for you | Verdict |
|---|---|---|---|
| [career-ops](https://github.com/career-ops-hq/career-ops) | End-to-end: scan, score, tailor, track, prep; stops before Submit | Good, if data is stored outside the VM | **Core** |
| [ai-job-search](https://github.com/ai-job-search-dev/ai-job-search) | End-to-end twin, Denmark-first sources | Good, but a heavier toolchain and no Finland | Replacement, not better |
| [JobSpy](https://github.com/speedyapply/JobSpy) | Scraper CLI/MCP: LinkedIn by location, Indeed Finland | Installs with pip; LinkedIn returns 429s on bursts | Optional later experiment only |
| [openings-mcp](https://github.com/amikai/openings-mcp) | One MCP server over many ATS boards | Duplicates career-ops providers; no Finnish boards | Skip |
| [Resume-Matcher](https://github.com/srbhr/Resume-Matcher), [Reactive Resume](https://github.com/reactive-resume/reactive-resume) | CV builders with web UIs | Need a web UI or a self-hosted database | Skip |
| [RenderCV](https://github.com/rendercv/rendercv) | Turns YAML into a PDF CV | Works, but career-ops already renders | Unnecessary |
| AIHawk → [invisible_dots](https://github.com/feder-cr/invisible_dots), [ApplyPilot](https://github.com/Pickle-Pixel/ApplyPilot), [jobpilot](https://github.com/suxrobGM/jobpilot), [Proficiently](https://github.com/proficientlyjobs/proficiently-claude-skills) | Auto-apply bots | Need a local Chrome; ApplyPilot has been stale for 7 months; the AIHawk URL now serves an unrelated anti-bot project | **Not usable, and risky** |
| [linkedin-mcp-server](https://github.com/stickerdaniel/linkedin-mcp-server) | Drives your logged-in LinkedIn session | Needs a browser login; its own docs warn of bans | Avoid |

The case against career-ops is real but not disqualifying. The project is **only 6.5 months old**, is run by a single lead maintainer with final say (a "benevolent dictator for life" model) ([GOVERNANCE.md](https://github.com/career-ops-hq/career-ops/blob/main/GOVERNANCE.md)), and changes fast enough that its own docs go stale. Its budget guide puts per-evaluation instructions at about 26k tokens ([RUNNING_ON_A_BUDGET.md](https://github.com/career-ops-hq/career-ops/blob/main/docs/RUNNING_ON_A_BUDGET.md)). Measured with the repo's own estimator, the real floor is **about 49k tokens**, and AGENTS.md alone accounts for about 21k ([context-budget.mjs](https://github.com/career-ops-hq/career-ops/blob/main/lib/context-budget.mjs)).

Its origin story is self-reported and internally inconsistent: "740 evaluated, 68 applied, 12 interviews, 1 offer". The author's own case study has hero-image alt text reading "516 evaluated offers" and a score distribution that sums to 195 ([santifer.io](https://santifer.io/career-ops-system)). The project's opt-in Hired Wall lists 17 hires, **none in the Nordics** ([HIRED.md](https://github.com/career-ops-hq/career-ops/blob/main/HIRED.md)).

The most relevant warning is an independent article reporting that a single default config keyword "was actively hiding every job I was qualified for" ([levelup.gitconnected](https://levelup.gitconnected.com/i-let-an-ai-agent-run-my-job-search-it-almost-erased-my-entire-career-with-one-keyword-a16df955ae43)). The shipped title filter is AI-centric ("AI", "ML", "LLM", "Agent"…), and the template itself warns that unlisted variants are "dropped in silence" ([portals.example.yml](https://github.com/career-ops-hq/career-ops/blob/main/templates/portals.example.yml)). An earlier bug that burned 33M tokens in under five minutes has been fixed ([issue #1235](https://github.com/career-ops-hq/career-ops/issues/1235)).

These caveats shape how you use career-ops, not whether you use it:

- Update only at tagged releases.
- Replace every default filter during onboarding.
- Keep sessions short.

Combining repos mostly duplicates work. JobSpy is the only add-on that widens reach, but it scrapes LinkedIn. LinkedIn's User Agreement §8.2 bans "crawlers, browser plugins and add-ons" that scrape the service ([LinkedIn User Agreement](https://www.linkedin.com/legal/user-agreement)). The best-known auto-applier's creator was banned and received legal threats ([ERE](https://newsletter.ere.net/p/what-it-means-to-apply-for-a-job-is-changing-0c55)). LinkedIn's own job-alert emails, read through your Gmail connector, give you the same leads without that exposure. Interview content repos such as [tech-interview-handbook](https://github.com/yangshun/tech-interview-handbook) and [system-design-primer](https://github.com/donnemartin/system-design-primer) are reference material Claude can consult on demand, not part of the workflow.

## Finnish coverage depends on a company list you must build

Finland's job channels are employer ATS boards, LinkedIn, Duunitori, Job Market Finland (Työmarkkinatori), The Hub, agencies and personal networks. The Finnish union of tech graduates, TEK, says **"only 20–30% of available jobs are made public"** ([TEK](https://www.tek.fi/en/services-and-benefits/job-search-and-career/tools-and-information-for-job-seekers/where-to-look-for-a-job-in-finland)). Oikotie Työpaikat has closed ([oikotie](https://tyopaikat.oikotie.fi/)). Few of these channels can be read by a tool, legally or at all:

| Channel | Machine access |
|---|---|
| The Hub | Open JSON API. A probe returned **182 Finnish postings** ([The Hub API](https://thehub.io/api/v2/jobsandfeatured?countryCode=FI&page=1)) |
| Duunitori | robots.txt disallows all user agents ([robots.txt](https://duunitori.fi/robots.txt)), and its terms forbid scraping ([terms](https://duunitori.fi/compliance/kayttoehdot)) |
| Työmarkkinatori | Search API needs a subscription key and IP allowlisting from KEHA-keskus ([KIPA docs](https://tyomarkkinatori.fi/jobpostingprovider/documentation/KIPA-search-jobpostings-fi.html)) |
| Jobly, LinkedIn | No open API |

The good news is that career-ops already reads the systems behind most English-language Finnish tech jobs. Live probes of public ATS APIs on 2026-10-22 mapped major employers to platforms career-ops supports:

| Employer | ATS (verified) | Postings: total / in Finland |
|---|---|---|
| Wolt | Greenhouse `wolt` ([API](https://boards-api.greenhouse.io/v1/boards/wolt/jobs)) | 200 / 21 |
| Supercell | Ashby `supercell` ([API](https://api.ashbyhq.com/posting-api/job-board/supercell)) | 39 / 29 |
| ICEYE | Ashby `iceye` ([API](https://api.ashbyhq.com/posting-api/job-board/iceye)) | 194 / 93 |
| Reaktor | Ashby `reaktor` ([API](https://api.ashbyhq.com/posting-api/job-board/reaktor)) | 19 / 15 |
| Solita | Greenhouse `solita` ([API](https://boards-api.greenhouse.io/v1/boards/solita/jobs)) | 62 / 30 |
| Smartly.io | Greenhouse `smartlyio` ([API](https://boards-api.greenhouse.io/v1/boards/smartlyio/jobs)) | 58 / 20 |
| Tieto | SmartRecruiters `Tieto2` ([API](https://api.smartrecruiters.com/v1/companies/Tieto2/postings?limit=100&country=fi)) | 61 in Finland |
| Vincit, Siili, Eficode, Columbia Road, Netum, Qvik | Teamtailor RSS (e.g. [siili](https://siili.teamtailor.com/jobs.rss)) | 2–7 each |
| Futurice | Teamtailor on a branded host (needs `provider: teamtailor`) ([careers.futurice.com](https://careers.futurice.com/)) | not counted |
| KONE, Fiskars, Unity | Workday (e.g. [KONE](https://kone.wd3.myworkdayjobs.com/en-US/Careers)) | not counted |
| Fortum, Wärtsilä, Vaisala | SAP SuccessFactors (e.g. [jobs.fortum.com](https://jobs.fortum.com/)) | not counted |
| Nokia | Oracle Recruiting Cloud ([jobs.nokia.com](https://jobs.nokia.com)) | not counted |

Yet the shipped template contains **one** Finnish company. Aiven is scanned by web search, and The Hub appears only as a commented-out example set to the whole EU ([portals.example.yml](https://github.com/career-ops-hq/career-ops/blob/main/templates/portals.example.yml)). The bottleneck is therefore your company list, not career-ops' providers. About 25 hand-verified entries, plus The Hub with `countryCode: FI`, would cover the main Finnish product companies and consultancies. The probes also exposed a trap: SmartRecruiters returns HTTP 200 with zero results even for slugs that don't exist, so a 200 is not proof that a company uses it.

Language needs deliberate handling. career-ops ships 20 language and market sets but **no Finnish one** ([modes/](https://github.com/career-ops-hq/career-ops/tree/main/modes)). The Danish set is not a substitute, because its legal and benefit vocabulary is specific to Denmark. Use the default English modes plus the generic [eu-swe.md](https://github.com/career-ops-hq/career-ops/blob/main/modes/regional/eu-swe.md) calibration, and let Claude read Finnish-language job descriptions directly. InfoFinland notes that applications are usually written "in the language in which the job advertisement was published" ([InfoFinland](https://infofinland.fi/work-and-enterprise/find-a-job-in-finland/job-application-and-cv)). So your profile should state your Finnish level and treat "suomen kielen taito" (Finnish language skill) requirements as a deal-breaker or a flag.

For Duunitori, Työmarkkinatori, LinkedIn and agencies, the compliant route is their own email alerts (Duunitori's is called Duunivahti) sent to a Gmail label. Claude reads that label through the connector and forwards promising roles into the pipeline. The career-ops aggregator rule applies to these leads: confirm each role on the employer's own ATS before treating it as live ([AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md)). This alert route is sound in principle but has not been tested.

## Enhancv's API renders and stores CVs; it does not tailor them

The Enhancv developer API is small: **six endpoints** to list, create (from structured JSON), retrieve, export to PDF, delete, and upload a PDF/DOC/DOCX for AI parsing ([Enhancv API docs](https://developers.enhancv.com/)). It has no update endpoint, no cover letters, no ATS score, no job-description tailoring, no translation and no published API spec. LinkedIn import is enabled by sales on request ([Import from LinkedIn](https://developers.enhancv.com/api/linkedin/)). Every "AI" feature Enhancv advertises lives in the consumer web app, not the API ([Enhancv pricing FAQ](https://enhancv.com/pricing/)). The API is a storage-and-rendering backend; the intelligence has to stay with Claude and career-ops.

The economics are lopsided. API keys require the Business plan, which starts at **$99/month**, against **$13.32/month for Pro** ([Enhancv help](https://help.enhancv.com/en/articles/11588544-what-is-the-difference-between-enhancv-pro-and-enhancv-business)). Rate limits (60 requests/minute) are irrelevant at personal scale ([Rate Limits](https://developers.enhancv.com/guides/rate-limits/)). A documented error example says "Your plan allows 5 resumes", which conflicts with the "unlimited" claim in the help center ([Create Resume](https://developers.enhancv.com/api/create/)). Monthly fees are non-refundable once used ([Terms](https://enhancv.com/terms/)).

Privacy deserves a conscious choice. The data controller is a Bulgarian company, but its servers are in the US, and the named sub-processors include OpenAI and HrFlow.ai ([Privacy](https://enhancv.com/privacy/)).

ATS evidence argues for single-column output. Enhancv's own testing claims a 96.73% parse score for all templates ([Enhancv blog](https://enhancv.com/blog/is-enhancv-ats-friendly/)). A competitor's test, against five major ATSs (Workday, Greenhouse, Lever, iCIMS, Taleo), found the Double Column template parsed cleanly on **1 of 5** systems and the single-column "Traditional" template on **5 of 5** ([Resume Optimizer Pro](https://resumeoptimizerpro.com/blog/resume-optimizer-pro-vs-enhancv)). Nobody has tested Enhancv PDFs on Teamtailor, Recruitee or SmartRecruiters, which are common in Finland.

That leaves Enhancv two useful jobs. The first is **importing your CV**. If your current CV already lives in Enhancv, `GET /resumes/:id` returns it as structured JSON ([Retrieve Resume](https://developers.enhancv.com/api/retrieve/)), and Claude can draft `cv.md` from it for you to confirm. Prefer this to the upload endpoint, whose AI parsing "may not be 100% accurate" and sends your file to HrFlow ([Upload Resume](https://developers.enhancv.com/api/upload/)).

The second job is **an optional styled CV variant**, produced like this:

1. career-ops tailors the CV and runs its fact and structure checks.
2. A mapper script of about 100–150 lines converts the payload to Enhancv's format, with `layout: "single"`, A4, `hideBranding: true` and every section in column 0.
3. Three curl calls create the resume, export the PDF and delete the resume. Your key comes from an environment secret.
4. `pdftotext` extracts the text, and career-ops' fact checker `verify-cv-facts.mjs` checks it against `cv.md`.

Do not replace career-ops' renderer with Enhancv. You would lose its section-order and chronology guards, its page limit and its deterministic ATS score, all of which run on career-ops' own HTML ([generate-pdf.mjs](https://github.com/career-ops-hq/career-ops/blob/main/generate-pdf.mjs)). Use plain curl rather than the only community MCP server, [kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv): it is two weeks old, has 0 stars and would hold your API key.

The authenticated round trip is still untested, because no key was available in the research container. Run it once early. If the styled variant adds nothing over career-ops' own A4 PDF, drop to Pro or cancel at your next renewal.

## Every session starts blank unless a private repo carries your state

Claude Code on the web starts each session on "a fresh virtual machine… with your repository cloned" ([cloud environments](https://code.claude.com/docs/en/cloud-environments)). That has three consequences:

- **Skills come from the repo.** Repo-level `.claude/skills/` load, so `/career-ops` is available in your fork automatically. User-level skills do not.
- **The default network blocks job boards.** The Default environment's "Trusted" network level reaches only package registries, GitHub and cloud SDKs, so the career-ops scanner fails unless the environment uses Custom or Full access ([access levels](https://code.claude.com/docs/en/cloud-environments#access-levels)). This research container reached Greenhouse, Ashby, Teamtailor, SmartRecruiters, The Hub and api.enhancv.com, so keep that environment's network setting.
- **Connectors are unaffected.** MCP connectors such as Gmail and Drive bypass the network allowlist entirely.

career-ops' own cloud guide is blunt about the rest. "A normal fork of this public repository is public, so do not use one for personal career data". Git-ignored files such as `cv.md`, `data/` and `reports/` are not saved when a session pushes, and you should "never force-add these paths" ([SETUP.md](https://github.com/career-ops-hq/career-ops/blob/main/docs/SETUP.md)).

The design that satisfies all of this uses **two repos**:

| Repo | Contents | Visibility |
|---|---|---|
| `realsanket/career-ops` (your fork) | Code only | Public |
| `realsanket/career-ops-data` (new) | `cv.md`, `config/profile.yml`, `modes/_profile.md`, `modes/_custom.md`, `portals.yml`, `data/`, `reports/`, `output/`, `jds/`, `interview-prep/` | **Private** |

Attach both repos to every session. Point career-ops at the data repo with the `CAREER_OPS_DATA_DIR` environment variable, or with the git-ignored `.career-ops-data` marker file. Both are resolved relative to the code repo's root ([path-resolver.mjs](https://github.com/career-ops-hq/career-ops/blob/main/path-resolver.mjs)). Once set, "all User Layer files" resolve there ([DATA_CONTRACT.md](https://github.com/career-ops-hq/career-ops/blob/main/DATA_CONTRACT.md)).

The override reaches both the scripts and the agent's own file writes. **102 of the 155 top-level scripts** reference the resolver, and JD captures also follow the data root (`JDS_DIR = join(DATA_ROOT, 'jds')` in `archive-posting.mjs`). The `/career-ops` skill router tells Claude to resolve every user-layer path against the data root, "never against the process's current working directory" ([SKILL.md](https://github.com/career-ops-hq/career-ops/blob/main/.claude/skills/career-ops/SKILL.md)). The shared mode rules require the same of reports and tracker additions ([_shared.md](https://github.com/career-ops-hq/career-ops/blob/main/modes/_shared.md)). Earlier in this conversation it was established that the fork matches upstream v1.37.0, that its full suite passes (16,801 tests) in this container, and that all personal files are git-ignored. The two-repo design itself has **not** been tested end to end.

There is a more conservative variant: replace the public fork with a private import, as SETUP.md prescribes. It removes the last leak path, which is a session committing personal text to a tracked file in a public repo. The repo's CI guard against committed user data is still advisory, not a required check ([issue #5587](https://github.com/career-ops-hq/career-ops/issues)). Keeping the public fork is defensible if you treat it as read-only code. It keeps one-click upstream sync and lets you contribute Finland improvements back.

Three habits make the design reliable:

- **Before you push or close a session, check both repos with `git status`.** The fork should show nothing changed. Anything personal there means a script ignored the data root.
- **Push the data repo before every session ends.**
- **Add a setup script that runs `npm ci` and `npx playwright install chromium`.** Installing Chromium and producing a PDF was verified in this container, but it is a 120 MiB download that every new VM must repeat.

## Claude drafts, scores and tracks; you network and press Submit

The table below separates what works in your cloud-only setup from what does not. Form filling is the clearest hard limit. Apply mode launches a visible browser window (`{"headless": false}`), and that launch failed in this container because the VM has no display ([apply-scope.mjs](https://github.com/career-ops-hq/career-ops/blob/main/apply-scope.mjs)). The mode's documented fallback is to work from pasted questions or screenshots ([apply.md](https://github.com/career-ops-hq/career-ops/blob/main/modes/apply.md)).

| Stage | What Claude can do here | What it cannot do |
|---|---|---|
| Finding jobs | Run the token-free `scan.mjs` over Finnish employers' Greenhouse, Ashby, Teamtailor, Workday, SuccessFactors, SmartRecruiters and Workable boards plus The Hub; triage job-alert emails via Gmail; turn company names into ATS entries with `discover` | Read Duunitori (its terms forbid it) or Työmarkkinatori (needs credentials); log into LinkedIn; count on Workday boards until tested (they refused plain HTTP in probes); reach the hidden 70–80% of the market except through outreach you send |
| Evaluating fit | Write a scored report on each role: 1–5 score, legitimacy check, JD archived verbatim; read Finnish JDs; check postings are still live via ATS APIs | Apply Finnish collective-agreement or benefit rules (no Finnish market mode); evaluate cheaply (about 49k tokens of instructions each); predict outcomes before `calibrate` has your data |
| CV and cover letter | Tailor A4 PDFs checked against `cv.md`, scored for ATS parsing, with an optional single-column ATS variant; write cover letters in the ad's language; optionally render an Enhancv variant | Add experience you don't have (blocked by design); keep career-ops' checks on Enhancv output without a `pdftotext` re-check |
| Applying | Draft answers to pasted form questions or screenshots; draft application emails | Fill or submit any form (no visible browser in the cloud, and career-ops never submits) |
| Tracking | Maintain `data/applications.md` with `set-status.mjs` in the private repo; mirror rows to Google Sheets on request | Keep anything you didn't push; sync to Drive automatically (no built-in sync) |
| Follow-ups | Compute due follow-ups (`followup`); classify replies read from Gmail (`paste-reply`, `reply-watch`); leave drafts in Gmail | Send anything on its own initiative; remind you between sessions (scheduled runs are untested here) |
| Interview prep | Research companies (`deep`), build prep plans, run text mock interviews, debrief, keep a story bank with sources | Run voice or video mocks; attend or follow up by phone |
| Salary and offer | Set a monthly-gross salary expectation (palkkatoive) from survey data; walk through contract clauses (`offer-prep`); draft negotiation replies | Give legal advice or verdicts on contracts |
| Work permit | Explain permits, check salary against the threshold, prepare a fast-track checklist | File in Enter Finland or prove your identity |

The Finland-specific numbers Claude should anchor on are solid.

**Salaries.** The Koodiklinikka developer survey, collected in February–March 2026 with 588 employees, gives these median monthly gross salaries ([Koodiklinikka](https://koodiklinikka.github.io/palkkakysely/2025/)):

| Group | Median monthly gross |
|---|---|
| All employees | **€5,800** (p25–p75: €4,900–6,900) |
| Helsinki region | **€6,000** |
| Senior | €5,800 |
| Staff/Principal/Lead | €6,840 |
| English-only working language | €6,561 |

Finnish employers ask for a salary expectation (palkkatoive) as a monthly gross figure, and it should be "not too high but not too low" ([InfoFinland](https://infofinland.fi/work-and-enterprise/find-a-job-in-finland/job-application-and-cv)).

**Interviews.** At Finnish consultancies they lean conversational. Reaktor describes "a 60-minute remote conversation… not a memory test" ([Reaktor](https://www.reaktor.com/trainees-2026/summer-developer-interview-process)), so prep should weight behavioural stories over LeetCode.

**Work permits.** If you are a non-EU citizen, the specialist permit and the EU Blue Card both require at least **€3,937/month in 2026**. The fee is €530 for an electronic application. A two-week fast track is available for first permits applied for from abroad ([Migri specialist](https://migri.fi/en/specialist); [Migri Blue Card](https://migri.fi/en/eu-blue-card)). Your employer adds its part in Enter Finland within two working days ([Migri fast track](https://migri.fi/en/fast-track)). career-ops' visa filter is tuned to US and UK "sponsorship" wording. In Finland, add positive keywords such as "relocation" and "residence permit" instead.

## Eleven steps from today to a calibrated weekly routine

The sequence puts infrastructure first. A cloud-only user who skips it loses work silently.

| When | Step | What happens | Done when |
|---|---|---|---|
| **Thu 22 Oct (today)** | 1. Build the workspace | Create the private repo `career-ops-data`. In the Claude Code environment settings, keep Full or Custom network access (include the ATS hosts, thehub.io and api.enhancv.com). Add `CAREER_OPS_DATA_DIR` pointing at the data repo clone, add `ENHANCV_API_KEY` as a secret, and add a setup script running `npm ci` and `npx playwright install chromium` | Settings saved |
| Thu 22 Oct | 2. Prove persistence | In a session with both repos attached, Claude runs `node doctor.mjs --json` (missing files should be reported in the data repo), writes a test file and pushes the data repo. A second, fresh session must see the file, and `git status` in the fork must stay clean | Round trip passes; stop and fix if not |
| Fri 23 Oct | 3. Load your CV | Paste it, put the PDF in Drive or in the data repo's `documents/` folder (`intake` mode), or pull your existing Enhancv resume as JSON. Claude writes `cv.md` with the heading layout described in AGENTS.md; you approve it line by line | `cv.md` approved and pushed |
| Fri 23 Oct | 4. Onboard for Finland | Claude runs `onboard-write.mjs` with software-engineering title keywords that **replace** the AI defaults; a location filter of Finland plus Helsinki, Espoo, Vantaa, Tampere, Turku, Oulu and Jyväskylä; EUR pay targets; English output. It then personalises `_profile.md` with your Finnish level, deal-breakers and permit status | `doctor.mjs` reports no unpersonalised files |
| Mon 26–Wed 28 Oct | 5. Build Finnish sources | Claude adds the verified employers above and The Hub with `countryCode: FI` to `portals.yml`, uses `discover` for more, then runs `scan.mjs` and `audit-portals.mjs`. You set up Duunivahti, a Työmarkkinatori saved search and LinkedIn and agency alerts into one Gmail label, and export LinkedIn `Connections.csv` for `linkedin-join.mjs` | Audit shows no empty or provider-less key employers |
| Thu 29–Fri 30 Oct | 6. First evaluations | Evaluate 3–5 top roles with `auto-pipeline`. Compare the scores with your own judgement and adjust `_profile.md` | You trust the scores |
| Week of 2 Nov | 7. First applications | Only roles scoring 4.0 or higher. Claude produces the career-ops A4 PDF and cover letter; run the one-time Enhancv round trip test (step 3 of the Enhancv flow above). You download files from the private repo, ask Claude for answers to pasted form questions, submit yourself, then mark the role `Applied` | Tracker updated and pushed |
| From 9 Nov, twice a week | 8. Routine | Early-week session: scan, triage alerts, evaluate, apply. Late-week session: `followup`, read replies from Gmail, write Gmail drafts, use `contacto` for outreach drafts and send open applications. Every session ends with `git status` and a push | Steady, low-volume pipeline |
| When an interview is booked | 9. Interview prep | Use `deep`, `interview-prep`, `interview/practice` and `debrief`; add sourced stories to the story bank | Prep doc in the data repo |
| When an offer arrives | 10. Offer and permit | Use `offer-prep` for the clause walk; benchmark against Koodiklinikka; check the €3,937 threshold and the Migri fast-track checklist | Decision made with the facts in hand |
| Mon 14 Dec, or after about 10 outcomes | 11. Calibrate | Run `patterns` and `calibrate` against real outcomes and retune targeting. Decide whether to keep the Enhancv Business plan or downgrade before renewal | Scores tied to evidence |

## Conclusion

Choosing a repo turns out to be the least important decision. What will decide this search is the hidden market that TEK puts at 70–80% of jobs, plus a hand-built list of Finnish employers, and no AI tool covers either. The Enhancv subscription matters least: it buys automation of a step career-ops already does for free, and its real value is a faster, cleaner way to import your CV.

The riskiest step is the one that looks most like plumbing. A cloud-only workflow without a verified, private, pushed data repo either loses work silently or, in a public fork, risks exposing it. Once your Finnish company list is verified, consider contributing it upstream, along with a Työmarkkinatori provider if KEHA-keskus grants API access. That is the missing piece that would make career-ops Finland-ready for everyone, and it would also be a public open-source contribution you can cite in your own applications.
