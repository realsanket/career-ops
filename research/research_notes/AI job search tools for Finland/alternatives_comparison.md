# Open-source alternatives and complements to career-ops for a Claude-assisted job search in Finland (cloud-only Claude Code on the web)

Checked on 2026-10-22. Repo metadata (stars, forks, open-issue counts, license, created and pushed dates, archived flag) comes from the GitHub search API through the session's GitHub connector. "Last commit" means the HEAD commit date of the default branch, read with a shallow `git clone` on the same day. Open-issue counts from the GitHub API include open pull requests. Claims marked "self-reported" or "README claims" come from the project itself and have not been independently verified.

## Q1. Which candidates exist, and how healthy are they? (verified metadata)

### Takeaway
career-ops (76.5k stars, commits daily) and a near-identical Claude Code framework, ai-job-search (63.2k stars, commits daily, Denmark-first), are the only two large, actively maintained, end-to-end "AI job search inside Claude Code" projects. Everything else either covers one stage (CV rendering, tailoring, job scraping, LinkedIn access, interview prep) or is stale. The original AIHawk auto-applier no longer exists at its URL. Its repo now redirects to an unrelated anti-bot agent project.

### Cited Findings

**Verified comparison table (2026-10-22)**

| Repo | Stars | Forks | Open issues+PRs | License | Last commit (default branch) | Latest tag / release | Status note |
|---|---|---|---|---|---|---|---|
| [career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops) (old URL santifer/career-ops resolves to the same HEAD `dff9703`) | 76,475 | 14,177 | 378 | MIT | 2026-10-21 (pushed 2026-10-22) | `package.json` 1.37.0 at HEAD. Remote tags include v1.4.0–v1.6.0 and web-v0.15.0 | Created 2026-04-04, very active |
| [ai-job-search-dev/ai-job-search](https://github.com/ai-job-search-dev/ai-job-search) (same HEAD `e16acee` as [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search)) | 63,165 | 19,498 | 55 | MIT | 2026-10-21 | Tagged releases per CHANGELOG (version not captured) | Created 2026-03-18, very active |
| [srbhr/Resume-Matcher](https://github.com/srbhr/Resume-Matcher) | 28,811 | 5,092 | 39 | Apache-2.0 | 2026-10-22 | v1.4.0 (tag commit 2026-10-22) | Active |
| [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) (formerly AmruthPillai/Reactive-Resume; Docker Hub still `amruthpillai/reactive-resume`) | 44,680 | 4,883 | 16 | MIT | 2026-10-22 | n/a | Active |
| [rendercv/rendercv](https://github.com/rendercv/rendercv) | 17,800 | 1,371 | 102 | MIT | 2026-03-25 (but pushed 2026-10-22 on other branches) | v2.8 (tag commit 2026-03-21) | Active, slower main-branch cadence |
| [xitanggg/open-resume](https://github.com/xitanggg/open-resume) | 8,938 | 1,038 | 145 | AGPL-3.0 | pushed 2024-10-29 | none | **Dormant for about 2 years** |
| [jsonresume/resume-cli](https://github.com/jsonresume/resume-cli) | 4,709 | 391 | 6 | MIT | pushed 2026-06-12 | — | **Archived.** Description: "MOVED to jsonresume/jsonresume.org (packages/cli)" |
| [jsonresume/jsonresume.org](https://github.com/jsonresume/jsonresume.org) (monorepo successor) | 336 | 67 | 54 | — | 2026-10-22 | — | Active |
| [speedyapply/JobSpy](https://github.com/speedyapply/JobSpy) | 4,535 | 897 | 33 | MIT | 2026-10-19 | v1.4.0 (2026-10-19) | Active |
| [feder-cr/Jobs_Applier_AI_Agent_AIHawk](https://github.com/feder-cr/Jobs_Applier_AI_Agent_AIHawk) → now [feder-cr/invisible_dots](https://github.com/feder-cr/invisible_dots) | 32,211 (inherited) | 4,731 | 6 | MIT | 2026-10-14 | none | **Repurposed.** The old AIHawk URLs (both `Jobs_Applier_AI_Agent_AIHawk` and `Auto_Jobs_Applier_AIHawk`) resolve to the same HEAD `ef69f5e` as invisible_dots, "a self-hosted alternative to OpenAI Dots… built to be undetectable by anti-bot systems". It is no longer a job applier |
| [Pickle-Pixel/ApplyPilot](https://github.com/Pickle-Pixel/ApplyPilot) | 1,745 | 628 | 81 | AGPL-3.0 | 2026-03-08 | none | **Stale for about 7 months** |
| [stickerdaniel/linkedin-mcp-server](https://github.com/stickerdaniel/linkedin-mcp-server) | 3,977 | 702 | 180 | Apache-2.0 | 2026-10-22 | releases (version not captured) | Active |
| [eliasbiondo/linkedin-mcp-server](https://github.com/eliasbiondo/linkedin-mcp-server) | 200 | 40 | 3 | — | not checked | — | — |
| [amikai/openings-mcp](https://github.com/amikai/openings-mcp) | 103 | 10 | 16 | MIT | 2026-09-22 | — | Active, young (created 2026-06-27) |
| [borgius/jobspy-mcp-server](https://github.com/borgius/jobspy-mcp-server) | 120 | 45 | 2 | — | 2026-03-13 | — | Stale. JobSpy now ships its own MCP server |
| [workopia/workopia-mcp](https://github.com/workopia/workopia-mcp) | 314 | 21 | 1 | — | 2026-08-31 | — | Hosted commercial MCP (HERAAI PTY LLC) |
| [varunr89/resume-tailoring-skill](https://github.com/varunr89/resume-tailoring-skill) | 792 | 134 | 8 | MIT | 2026-02-28 | — | Stale for about 8 months |
| [proficientlyjobs/proficiently-claude-skills](https://github.com/proficientlyjobs/proficiently-claude-skills) | 429 | 74 | 4 | — | 2026-03-12 | — | Stale. Vendor funnel for the paid Proficiently service |
| [ARPeeketi/claude-resume-kit](https://github.com/ARPeeketi/claude-resume-kit) | 295 | 58 | 0 | — | 2026-03-09 | — | Stale, academic-oriented |
| [javiera-vasquez/claude-code-job-tailor](https://github.com/javiera-vasquez/claude-code-job-tailor) | 170 | 41 | 1 | — | not checked | — | — |
| [yanliudesign/job-description-skill](https://github.com/yanliudesign/job-description-skill) | 115 | 15 | 0 | — | not checked | — | JD → HTML report skill |
| [SankaiAI/ats-optimized-resume-agent-skill](https://github.com/SankaiAI/ats-optimized-resume-agent-skill) | 109 | 9 | 1 | — | not checked | — | DOCX resume skill |
| [suxrobGM/jobpilot](https://github.com/suxrobGM/jobpilot) | 97 | 22 | 21 | — | 2026-10-06 (v2.2.1) | v2.2.1 | Active, auto-apply |
| [Stupidoodle/swissdevjobs-cli](https://github.com/Stupidoodle/swissdevjobs-cli) | 103 | 12 | 1 | — | not checked | — | Covers 7 countries (CH, DE, UK, US, CA, NL, FR). **No Finland** |
| [nicolomantini/LinkedIn-Easy-Apply-Bot](https://github.com/nicolomantini/LinkedIn-Easy-Apply-Bot) | 1,156 | 416 | 0 | — | 2026-10-07 | — | LinkedIn auto-apply bot |
| [wodsuz/EasyApplyJobsBot](https://github.com/wodsuz/EasyApplyJobsBot) | 831 | 225 | 62 | — | 2026-03-29 | — | Selenium auto-login and auto-apply bot |
| [GodsScion/Auto_job_applier_linkedIn](https://github.com/GodsScion/Auto_job_applier_linkedIn) | not checked | — | — | — | 2026-09-10 | — | LinkedIn auto-apply bot |
| [anthropics/skills](https://github.com/anthropics/skills) (official) | 182,862 | 21,656 | 1,425 | — | 2026-10-09 | — | Skills: docx, pdf, pptx, xlsx, doc-coauthoring, skill-creator, and others. **No job-search or resume skill** |
| [yangshun/tech-interview-handbook](https://github.com/yangshun/tech-interview-handbook) | 143,104 | 16,867 | 37 | MIT | 2026-08-07 | — | Maintained |
| [donnemartin/system-design-primer](https://github.com/donnemartin/system-design-primer) | 375,093 | 58,945 | 630 | "Other" (NOASSERTION per GitHub) | pushed 2026-09-15 | — | Maintained |
| Discovery lists: [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) 77,647 · [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) 56,224 · [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) 36,152 | | | | | | | Lists only |

- Third-party listings report career-ops star counts inconsistently (9.1K, 69K+, 73,000+) and point to both santifer/career-ops and career-ops-hq/career-ops — [WebSearch summary of career-ops coverage](https://themenonlab.blog/blog/career-ops-ai-job-search-claude-code-skill). Today's verified figure is 76,475, and the old URL resolves to the same repo — [career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops).
- The ai-job-search README says it was built by a geophysicist after his position was cut in late 2025, and self-reports "69 tailored applications, 20 first interviews, and one signed contract" — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search). This is single-user and self-reported.
- The career-ops origin story (740 listings evaluated, 68 applied, 12 interviews, 1 offer) is also self-reported. One write-up notes that the job accepted came inbound — [Career-Ops write-up](https://themenonlab.blog/blog/career-ops-ai-job-search-claude-code-skill); [AGENTS.md origin section](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- Searches found no maintained open-source "Jobright-style" clone with meaningful adoption. ApplyPilot copycats (yvonnehe772/applypilot 296 stars, ibarrajo/ApplyPilot 23 stars) and AIHawk re-uploads (ElephantPrinceDev/Jobs_Applier_AI_Agent_AIHawk 6 stars, mujtabasiddiqui0786 1 star) are small forks or clones — [GitHub search "applypilot"](https://github.com/search?q=applypilot&type=repositories); [GitHub search "Jobs_Applier_AI_Agent"](https://github.com/search?q=Jobs_Applier_AI_Agent&type=repositories).

### Inferences
- Both 2026-born frameworks went from zero to more than 60k stars in about 7 months. Popularity cannot be independently validated (star inflation is possible), but commit activity is real and daily for both. Neither should be judged on stars alone.
- AIHawk should be dropped from consideration. The code at the famous URL is a different product, and the surviving copies are unmaintained re-uploads.
- open-resume and JSON Resume `resume-cli` should be treated as legacy. RenderCV and Reactive Resume are the live CV-rendering options.

### Gaps
- Release dates for career-ops' newest version could not be pinned. The GitHub releases API was blocked for non-session repos, and the v* tags visible through `git ls-remote` stop at v1.6.0 while `package.json` says 1.37.0, so the release-tag naming scheme is unclear.
- Star counts for GodsScion/Auto_job_applier_linkedIn were not checked. Last commit dates for a few small skill repos were not checked.
- Star authenticity (bot-starring) cannot be verified with available tools.

## Q2. Which job-search stages does each candidate cover? Which are replacements and which are complements?

### Takeaway
Only ai-job-search is a true replacement for career-ops: same shape (Claude Code skills, fit scoring, tailored LaTeX CV and cover letter, interview prep, tracker, Gmail sync, never auto-submits). Everything else is a complement covering one stage. Most of those stages are already covered inside career-ops, so the real gaps are Finland-specific job sources and possibly a nicer CV renderer.

### Cited Findings
- **career-ops**: scans boards, scores each job 1–5 against your CV, tailors an ATS-friendly resume and cover letter, interview prep, application tracker. "It helps you fill in each application; you press Submit" — [repo description](https://github.com/career-ops-hq/career-ops). Its AGENTS.md lists modes for evaluation, CV PDF, LaTeX, cover letter, contacto (LinkedIn outreach drafts), interview-prep, followup, reply-watch (email reply classification), patterns, upskill, and offer-prep — [AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- **ai-job-search**: `/setup` builds the profile from documents, a pasted CV, or an interview. `/scrape` and `/rank` find and shortlist jobs. `/apply <url>` scores fit on five dimensions with deal-breakers and a language gate, then drafts a LaTeX CV and cover letter, has a separate reviewer agent critique them, and checks PDFs visually and for ATS parseability. `/interview` gives stage-specific prep and a mock interview. `/outcome`, `/gmail-sync` (proposes status updates for approval), `/notion-sync`, `/html-report`, `/expand`, `/upskill`, `/add-portal`. Follow-ups are "drafts only, never sends" — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search).
- **ai-job-search job sources**: Denmark is primary (Jobindex, Jobnet, Akademikernes Jobbank, Jobdanmark). Country-agnostic `linkedin-search` uses LinkedIn's public guest endpoints ("personal use only"). `freehire-search` uses freehire.me's public API. `/add-portal` generates a portal skill for any local board. Finland is not mentioned — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search).
- **Resume-Matcher**: an "AI harness for building resumes, PDFs, cover letters" with a FastAPI backend, a Next.js frontend, and SQLite, run locally or in Docker. It has an MCP server so Claude Code can write the tailored resume while Resume-Matcher stores, checks, and renders it — [Resume-Matcher README](https://github.com/srbhr/Resume-Matcher).
- **Reactive Resume**: a resume builder with an AI assistant, PDF checks, a REST API and MCP server "for document management, imports, exports, checks, and application workflows". Hosted app at rxresu.me, or self-host with Docker/Vercel/Cloudflare — [reactive-resume README](https://github.com/reactive-resume/reactive-resume).
- **RenderCV**: "Write your CV or resume as YAML, then run RenderCV" → PDF, with a JSON Schema and themes (classic, moderncv, ink). Typst-based per repo topics — [rendercv README](https://github.com/rendercv/rendercv).
- **JobSpy**: a jobs scraper library for LinkedIn, Indeed, Glassdoor, ZipRecruiter, Bayt, Naukri, BDJobs, and HelloWork (Google is listed but noted as unavailable). It has a `jobspy` CLI with JSON-lines output and an MCP server `mcp-jobspy` (`uvx mcp-jobspy@latest`) — [JobSpy README](https://github.com/speedyapply/JobSpy).
- **openings-mcp**: one MCP server for job boards (LinkedIn, Indeed public search, Jobindex DK, and others) plus ATS career sites for "41,000+ companies": Workday, Ashby, Greenhouse, Lever, Teamtailor, Recruitee, SmartRecruiters, Workable, SuccessFactors, iCIMS, Oracle, JOIN, BambooHR, and others. It "never logs in" and uses public endpoints. Runs over local stdio (Go binary, Homebrew, or Docker) — [openings-mcp README](https://github.com/amikai/openings-mcp).
- **Workopia MCP**: a hosted remote MCP (`https://workopia.io/api/mcp-jobs`) with OAuth sign-in. Its `job_tool` searches "millions of live jobs across 90+ countries (employer career pages + ATS feeds — Lever, Greenhouse, Workday)". It also does resume tailoring and cover letters. Activity "may be associated with your Workopia profile". Free at launch — [workopia-mcp README](https://github.com/workopia/workopia-mcp).
- **stickerdaniel/linkedin-mcp-server** tools: `search_jobs`, `get_job_details`, `get_job_apply_url`, `get_saved_jobs`, person and company profiles, `search_people`, `connect_with_person`, inbox, and `send_message` — [linkedin-mcp-server README](https://github.com/stickerdaniel/linkedin-mcp-server).
- **ApplyPilot**: six stages (discover via JobSpy plus 48 Workday portals and about 30 career sites → enrich → score 1–10 → tailor → cover letter → auto-apply), with Claude Code driving Chrome to submit — [ApplyPilot README](https://github.com/Pickle-Pixel/ApplyPilot).
- **jobpilot**: "applies to jobs for you". Searches LinkedIn, Indeed, Hiring Cafe and others, scores jobs, and runs "Auto-apply" campaigns "up to your limit" in a browser on your machine — [jobpilot README](https://github.com/suxrobGM/jobpilot).
- **Proficiently skills**: setup, job-search, tailor-resume, cover-letter, network-scan (LinkedIn contacts), and apply (fills Greenhouse/Lever/Workday forms). Requires the Claude in Chrome extension and Chrome. Promotes the paid Proficiently service — [proficiently README](https://github.com/proficientlyjobs/proficiently-claude-skills).
- **resume-tailoring-skill**: a Claude Code skill for tailored resumes "while maintaining factual integrity". It does experience discovery by interview, confidence-scored content selection with gap identification, and MD/DOCX/PDF output — [resume-tailoring-skill README](https://github.com/varunr89/resume-tailoring-skill).
- **Interview prep complements**: tech-interview-handbook ("Curated coding interview preparation materials for busy software engineers") and system-design-primer ("Learn how to design large-scale systems… Includes Anki flashcards") — [tech-interview-handbook](https://github.com/yangshun/tech-interview-handbook); [system-design-primer](https://github.com/donnemartin/system-design-primer).
- **Official Anthropic skills**: docx, pdf, pptx, xlsx, doc-coauthoring, and others. None is job- or resume-specific — [anthropics/skills tree](https://github.com/anthropics/skills/tree/main/skills).

**Stage coverage matrix** (✔ = covered, ~ = partial, — = no)

| Tool | Find jobs | Evaluate fit | Tailor CV | Cover letter | Track | Interview prep | Auto-submit | Role vs career-ops |
|---|---|---|---|---|---|---|---|---|
| career-ops | ✔ (ATS/API providers) | ✔ | ✔ (HTML/PDF and LaTeX) | ✔ | ✔ | ✔ | — (stops before Submit) | baseline |
| ai-job-search | ✔ (DK boards, LinkedIn guest, freehire, add-portal) | ✔ | ✔ (LaTeX + reviewer agent) | ✔ | ✔ (+ Gmail/Notion sync) | ✔ (+ mock) | — | **Replacement** |
| Resume-Matcher | — | ~ (match score) | ✔ | ✔ | — | — | — | Complement or overlap |
| Reactive Resume | — | — | ✔ (builder + AI) | ~ | ~ | — | — | Complement (CV editor) |
| RenderCV | — | — | render only | — | — | — | — | Complement (renderer) |
| JobSpy / mcp-jobspy | ✔ (incl. Indeed Finland) | — | — | — | — | — | — | Complement (source) |
| openings-mcp | ✔ (ATS incl. Teamtailor/Recruitee) | — | — | — | — | — | — | Complement (source) |
| Workopia MCP | ✔ | ~ | ~ | ~ | ~ | — | — | Complement (hosted, commercial) |
| LinkedIn MCP (stickerdaniel) | ✔ (LinkedIn) | — | — | — | — | — | — (but can message/connect) | Complement, ToS risk |
| ApplyPilot / jobpilot / Easy-Apply bots | ✔ | ✔ | ✔ | ✔ | ~ | — | **✔** | Replacement of a different, risky kind |
| tailoring skills (varunr89, claude-resume-kit, etc.) | — | ~ | ✔ | ~ | — | ~ | — | Overlap with career-ops |
| tech-interview-handbook, system-design-primer | — | — | — | — | — | ✔ (content) | — | Complement (content) |

### Inferences
- For a Finland-focused software engineer, the stages career-ops lacks are not CV tailoring or tracking, which it covers in depth. The gap is Finnish job discovery (see Q6). JobSpy (Indeed Finland plus LinkedIn by location) and openings-mcp (Teamtailor/Recruitee/SmartRecruiters/Workable endpoints, which many Nordic employers use) are the closest open-source fillers.
- Running ai-job-search and career-ops together would mostly duplicate work. Pick one as the "brain". ai-job-search's `/add-portal` generator and its Gmail-sync approval flow are the features most worth borrowing.

### Gaps
- The full ATS company roster in openings-mcp was not inspected for Finnish employers.
- Whether ai-job-search's `freehire-search` aggregator carries Finnish postings was not verified.

## Q3. Does each tool work when the user only chats with Claude in Claude Code on the web (ephemeral VM, fresh clone, no local GUI, no persistent disk)?

### Takeaway
Pure-Markdown/Node skill frameworks (career-ops, ai-job-search) and pip/uv-installable CLIs (JobSpy, RenderCV) are the only categories that fit a cloud-only workflow. Even these need two things. First, the environment's network access must be widened beyond the default **Trusted** allowlist to reach job boards. Second, personal data must persist somewhere other than the ephemeral VM. Tools that need a local Chrome profile, a logged-in browser session, a GUI web app, or a self-hosted database are poor fits.

### Cited Findings
- Cloud sessions run on "a fresh virtual machine (VM) running Ubuntu 24.04… with your repository cloned". "Cloud sessions start from a fresh clone of your repository. Anything you commit to the repo is available." — [Claude Code cloud environments docs](https://code.claude.com/docs/en/cloud-environments).
- The Default environment uses **Trusted** network access: "sessions reach package registries and other allowlisted domains, and nothing else". The Trusted list is "package registries, GitHub, cloud SDKs" plus Anthropic domains. **Full** allows any domain, and **Custom** takes your own allowlist — [cloud environments docs](https://code.claude.com/docs/en/cloud-environments#access-levels).
- Whatever the network level, sessions can still reach GitHub (separate proxy), "MCP connectors you enable, whose traffic travels through Anthropic's servers", and the Anthropic API — [cloud environments docs](https://code.claude.com/docs/en/cloud-environments#access-levels).
- User-level `~/.claude` skills, user-scoped MCP servers, and plugins enabled in settings are not available in cloud sessions. Repo `.claude/skills/`, a project-scoped `.mcp.json`, and CLAUDE.md are. "Interactive auth like AWS SSO… Not supported. SSO requires browser-based login that can't run in a cloud session" — [cloud environments docs](https://code.claude.com/docs/en/cloud-environments).
- Docker is available in cloud sessions. PostgreSQL and Redis are pre-installed but not running. Setup scripts and an environment cache can pre-install packages — [cloud environments docs](https://code.claude.com/docs/en/cloud-environments).
- career-ops documents a "Browser-only — Claude Code on the web" path. It says to put career-ops in a **private** GitHub repo (via GitHub Importer) because "A normal fork of this public repository is public, so do not use one for personal career data". `cv.md`, runtime `data/`, and `reports/*.md` are git-ignored, so "a normal web-session branch push does **not** persist them to GitHub: a new cloud session starts from the repository again, without the ignored files from the previous VM." It also says "Never force-add these paths" — [career-ops docs/SETUP.md](https://github.com/career-ops-hq/career-ops/blob/main/docs/SETUP.md) (read locally at HEAD `dff9703`).
- The user's fork **realsanket/career-ops is a public fork** (`fork: true`, `private: false`, `visibility: public`, created 2026-10-22) — [realsanket/career-ops](https://github.com/realsanket/career-ops) (GitHub search API, 2026-10-22).
- career-ops supports a data-root override (`CAREER_OPS_ROOT` / `CAREER_OPS_DATA_DIR` env var or a `.career-ops-data` marker file) so user data can live outside the code checkout — [AGENTS.md "Path Resolution Override"](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- ai-job-search also warns "A fork of this repo is always public — GitHub does not allow private forks of public repos" and recommends a private repo with the project as `upstream`. It requires Python 3.10+, Bun, and a LaTeX distribution with lualatex/xelatex — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search).
- Resume-Matcher needs Node 24+, uv, Python 3.13+, and runs a web UI. Its "Claude subscription (via Claude Code)" provider runs your installed `claude` CLI and is "not available inside the Docker images". The README warns that Anthropic "doesn't allow third-party apps to route requests through Claude Free/Pro/Max plans, this option may count as one" — [Resume-Matcher README](https://github.com/srbhr/Resume-Matcher).
- Reactive Resume self-hosting runs `docker compose up -d --build` to "start PostgreSQL, Redis, and SeaweedFS". The hosted app is rxresu.me — [reactive-resume README](https://github.com/reactive-resume/reactive-resume).
- stickerdaniel/linkedin-mcp-server uses your own LinkedIn login. It imports a session from a local Chromium-based browser or opens a login window. Sessions are stored in `~/.linkedin-mcp/profile/`. The Docker variant needs a one-time login through a browser viewer on port 6080. It recommends a proxy in your own country if the server runs on a VPS — [linkedin-mcp-server README](https://github.com/stickerdaniel/linkedin-mcp-server).
- ApplyPilot needs Python 3.11+, Node 18+, Chrome/Chromium, a Gemini API key (or OpenAI/local), and optionally a CapSolver key for CAPTCHAs — [ApplyPilot README](https://github.com/Pickle-Pixel/ApplyPilot). Proficiently requires the Claude in Chrome extension and Chrome running — [proficiently README](https://github.com/proficientlyjobs/proficiently-claude-skills). jobpilot works "in a normal browser window on your computer, signed in as" you — [jobpilot README](https://github.com/suxrobGM/jobpilot).
- JobSpy requires Python 3.10+, installs via pip or uvx, and ships a CLI and an MCP server — [JobSpy README](https://github.com/speedyapply/JobSpy). openings-mcp ships a Go binary or Docker image with no API keys — [openings-mcp README](https://github.com/amikai/openings-mcp).
- Workopia is a hosted remote MCP with OAuth (no API key), and Claude Code opens the OAuth flow in a browser on first use — [workopia-mcp README](https://github.com/workopia/workopia-mcp).

**Cloud-fit summary**

| Tool | Own API key? | Needs DB/Docker? | Needs browser/GUI? | Cloud-session fit |
|---|---|---|---|---|
| career-ops | No (runs on Claude) | No | Playwright only for PDF and liveness fallback | **Good**, but needs a private repo or external data persistence and a wider network level |
| ai-job-search | No | No | No (needs LaTeX + Bun install) | **Good**, same caveats. LaTeX install belongs in a setup script |
| JobSpy (CLI/MCP) | No | No | No | **Good** with Custom/Full network. LinkedIn returns 429 on bursts |
| openings-mcp | No | No (Docker optional) | No | **Good** via project `.mcp.json` + binary/Docker in setup script (inference) |
| RenderCV | No | No | No | **Good** (pip install) |
| Resume-Matcher | Yes unless Ollama or coding-agent mode | SQLite (+ optional Docker) | Web UI | Poor/awkward |
| Reactive Resume (self-host) | Optional AI key | Postgres + Redis + SeaweedFS | Web UI | Poor. The hosted rxresu.me plus its MCP is the only practical path (not verified for cloud) |
| Workopia MCP | No (OAuth account) | No | OAuth browser login once | Possible as a remote MCP connector, but a third-party commercial service holds your data |
| LinkedIn MCP | No | No | Needs a logged-in LinkedIn session | Poor, and risky |
| ApplyPilot / jobpilot / Proficiently / Easy-Apply bots | Gemini/OpenAI etc. (ApplyPilot) | No | **Yes**, local Chrome | **Not usable** cloud-only |

### Inferences
- The user's current setup (a public fork) is unsafe for personal data. Any personal file committed to realsanket/career-ops becomes public. Two safer patterns are worth weighing. (a) Import career-ops into a **private** repo, as career-ops' own SETUP.md recommends. Note that ignored files still won't persist unless the user deliberately un-ignores them in the private repo, which SETUP.md advises against for the shared template. (b) Keep code in the public fork and point `CAREER_OPS_ROOT` at a second, **private** data repo attached to the same cloud session. Google Drive/Sheets connectors (which bypass the network allowlist) could be another persistence layer, but career-ops has no built-in Drive sync.
- Because MCP connector traffic bypasses the allowlist, the user's existing Gmail connector is the most cloud-friendly way to feed career-ops' `reply-watch` / `paste-reply` flow. The same holds for ai-job-search's `/gmail-sync`.
- The career-ops scanners (`scan.mjs`) and JobSpy both make direct HTTP calls from the VM, so they will fail under the default Trusted level. The user must set Custom (listing ATS and job-board domains) or Full network access.

### Gaps
- It was not verified whether Claude's built-in WebFetch/WebSearch tools in a cloud session go through the environment allowlist. They worked in this research session, but the network level of this environment wasn't inspected.
- Whether Playwright/Chromium can run in the cloud VM without a setup script was not tested (the docs list chromedriver among the Node tooling).

## Q4. Ethics and ToS risk: mass-apply and LinkedIn automation

### Takeaway
LinkedIn's User Agreement explicitly bans bots, scrapers, and browser add-ons that automate activity or scrape data. The best-known open-source auto-applier (AIHawk) led to the creator's account being restricted and to legal threats, and he removed all LinkedIn features. Auto-apply tools (ApplyPilot, jobpilot, Easy-Apply bots) and session-based LinkedIn MCP servers carry real account-ban risk. career-ops and ai-job-search are designed to stop before Submit.

### Cited Findings
- LinkedIn User Agreement §8.2 (effective November 3, 2025). You may not "Develop, support or use software, devices, scripts, robots or any other means or processes (such as crawlers, browser plugins and add-ons or any other technology) to scrape or copy the Services, including profiles and other data from the Services". You also may not "Use bots or other unauthorized automated methods to access the Services, add or download contacts, send or redirect messages… or otherwise drive inauthentic engagement" — [LinkedIn User Agreement](https://www.linkedin.com/legal/user-agreement).
- Semafor (2024-09-12) reports that Federico Elia built a bot that could apply to about 1,000 jobs in two days. LinkedIn later restricted his account for "repeatedly sharing content that facilitates access to tools that automate activity on LinkedIn" — [Semafor](https://semafor.com/article/09/12/2024/linkedins-have-nots-and-have-bots).
- ERE newsletter (2025-07-16): AIHawk had more than 28,000 stars. LinkedIn said it does not "permit the use of third-party software (e.g. bots) that automates activity on LinkedIn". Elia "received legal threats and was banned from the platform". "In January" (context implies 2025) he removed all LinkedIn-related features, then launched the commercial Laboro. Per its co-founder, the average Laboro user applied to about 200 jobs, and half applied to every AI-suggested match — [ERE Weekly](https://newsletter.ere.net/p/what-it-means-to-apply-for-a-job-is-changing-0c55).
- The same ERE piece cites Greenhouse data: 22% of U.S. job seekers (31% of Gen Z) have used an AI agent to apply, and the average recruiter receives 270% more applications than three years ago — [ERE Weekly](https://newsletter.ere.net/p/what-it-means-to-apply-for-a-job-is-changing-0c55).
- The stickerdaniel LinkedIn MCP FAQ says LinkedIn's User Agreement prohibits automated access, accounts using automated tools "can be restricted or banned", and there is "no guarantee of account safety". It asks users to keep volume low and use one active session — [linkedin-mcp-server README](https://github.com/stickerdaniel/linkedin-mcp-server).
- ai-job-search's `linkedin-search` uses LinkedIn's public guest endpoints, labelled "personal use only" — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search). JobSpy also scrapes LinkedIn and warns of 429 rate limits and suggests proxies for larger searches — [JobSpy README](https://github.com/speedyapply/JobSpy).
- ApplyPilot auto-submits, with an optional CAPTCHA-solving key (CapSolver). Its README contains no explicit job-board ToS warning, only a warning about unaffiliated sites using the name — [ApplyPilot README](https://github.com/Pickle-Pixel/ApplyPilot).
- career-ops rule: "NEVER submit an application without the user reviewing it first… always STOP before clicking Submit/Send/Apply". It strongly discourages applying below 4.0/5. It also has a LinkedIn guard: one browser attempt per posting, no retries via guest endpoints, alternate accounts, or anti-bot workarounds — [AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- feder-cr's current flagship (the former AIHawk repo) markets itself as "Built to be undetectable by anti-bot systems", and a sibling `invisible_playwright_mcp` carries `job-hunting` and `job-search` topics — [feder-cr/invisible_dots](https://github.com/feder-cr/invisible_dots); [feder-cr/invisible_playwright_mcp](https://github.com/feder-cr/invisible_playwright_mcp).
- Vendor blogs claim LinkedIn restrictions are "usually temporary". One secondhand figure says 23% of LazyApply-style extension users were restricted within 90 days. These sources have commercial stakes and the figure is unverified — [FastApply blog](https://blog.fastapply.co/can-you-get-banned-for-auto-applying-on-linkedin-2026); [Scoutify](https://scoutify.com/blog/linkedin-auto-apply/).

### Inferences
- In a small market like Finland, where tech recruiters and hiring managers often know each other, mass auto-applying carries reputational cost on top of ToS risk. This is an inference, not sourced.
- The lowest-risk LinkedIn use is manual. Read postings yourself or paste JD text, and use LinkedIn only for human outreach that career-ops' `contacto` mode drafts but does not send.

### Gaps
- No primary-source data was found on actual LinkedIn ban rates for job-search MCP servers or guest-endpoint scraping.
- Indeed's and Glassdoor's ToS were not fetched. JobSpy scrapes both, and their terms likely restrict scraping, but this was not verified.

## Q5. Quality concerns: fabrication risk, spam, abandoned forks

### Takeaway
career-ops has the most explicit, enforced anti-fabrication design found: a source-of-truth file boundary, provenance markers, and fact-gates on CV output. ai-job-search and claude-resume-kit make similar claims. Auto-apply tools optimise for volume, and several small skills are already stale.

### Cited Findings
- career-ops: user-facing content is generated "exclusively" from `cv.md`, `article-digest.md`, `config/profile.yml`, `modes/_profile.md` and the user's own statements. "Keywords get reformulated, never fabricated". Authorship claims are "non-negotiable". Story-bank numbers need provenance markers. Tools include `generate-latex.mjs` (a fact gate), `cv-title-check.mjs`, `verify-cv-structure.mjs`, and `keyword-match.mjs` ("never injects keywords") — [AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- ai-job-search: "All claims in the CV and cover letter are verified against your actual profile". Unsupported keywords are shown as gaps, and `/interview` gives honest bridge answers. It also notes prompt-injection defences "are instruction-level, not a sandbox" — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search).
- claude-resume-kit: "Anti-fabrication by design. Provenance flags on every achievement… Verb discipline rules prevent overclaiming. A corrections log…" — [claude-resume-kit README](https://github.com/ARPeeketi/claude-resume-kit).
- ApplyPilot says tailoring "never fabricates" and preserves `resume_facts`, while still auto-submitting at volume — [ApplyPilot README](https://github.com/Pickle-Pixel/ApplyPilot).
- Staleness: ApplyPilot (last commit 2026-03-08), resume-tailoring-skill (2026-02-28), proficiently (2026-03-12), claude-resume-kit (2026-03-09), borgius/jobspy-mcp-server (2026-03-13), open-resume (pushed 2024-10-29), jsonresume/resume-cli (archived) — shallow-clone HEAD dates and GitHub API, 2026-10-22 ([ApplyPilot](https://github.com/Pickle-Pixel/ApplyPilot), [resume-tailoring-skill](https://github.com/varunr89/resume-tailoring-skill), [proficiently](https://github.com/proficientlyjobs/proficiently-claude-skills), [claude-resume-kit](https://github.com/ARPeeketi/claude-resume-kit), [jobspy-mcp-server](https://github.com/borgius/jobspy-mcp-server), [open-resume](https://github.com/xitanggg/open-resume), [resume-cli](https://github.com/jsonresume/resume-cli)).
- Product Hunt commenters on career-ops questioned how its scoring dimensions are weighted and warned that a bad filter config can surface excluded roles. These are questions, not demonstrated flaws, and come from a search summary, not a fetched page — [Product Hunt: career-ops on Claude](https://www.producthunt.com/posts/career-ops-on-claude).
- No rigorous independent evaluation was found of whether career-ops scoring predicts interviews or offers. Coverage is mostly promotional — [WebSearch summary](https://decodeops.substack.com/p/career-ops-the-terminal-that-replaced). career-ops itself ships a `calibrate` mode for checking scores against the user's own outcomes — [AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).

### Inferences
- For a user who wants fewer, high-quality applications in a small market, career-ops' guardrails are a strength and a reason to keep it as the core.
- The anti-fabrication rules are prompt-level (LLM instructions plus some deterministic checks), not guarantees. The user should still review every CV diff against `cv.md`.

### Gaps
- No independent study compares fabrication rates across these tools.

## Q6. Finland coverage: which tools actually reach Finnish job sources?

### Takeaway
None of the candidates has first-class Finland support. career-ops covers the ATS platforms Finnish tech employers commonly use (Teamtailor, Recruitee, Workable, SmartRecruiters, Greenhouse, Lever, Ashby, Workday, Personio) but has no provider for Finland's national boards (Duunitori, Työmarkkinatori/Job Market Finland) and ships almost no Finnish companies in its example portals. JobSpy reaches Indeed Finland and LinkedIn-by-location. Työmarkkinatori has an official search API that requires onboarding. Duunitori has no public API, only third-party scrapers.

### Cited Findings
- The career-ops `providers/` directory includes teamtailor, recruitee, workable, smartrecruiters, personio, greenhouse, lever, ashby, workday, thehub, and platsbanken (Sweden), among others. No provider for Duunitori, Työmarkkinatori, or jobs.fi was found. "Helsinki" appears once in `templates/portals.example.yml` (one company). `modes/regional/` contains only `eu-swe.md`. There is no Finnish market mode in the AGENTS.md language table — [career-ops providers/](https://github.com/career-ops-hq/career-ops/tree/main/providers) (local grep at HEAD `dff9703`); [AGENTS.md Language Modes](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- JobSpy: Finland is on the Indeed country list (`country_indeed`) but not marked as supported for Glassdoor. LinkedIn searches globally by `location`. Most endpoints cap at about 1,000 jobs per search — [JobSpy README](https://github.com/speedyapply/JobSpy).
- Työmarkkinatori (the Finnish public employment service's job market) documents an official job-posting search API (P67, OpenAPI specs) offered through the KEHA Centre's Kipa integration platform. Access appears to require an onboarding process. Unofficial Apify scrapers also exist — [Työmarkkinatori search API docs](https://tyomarkkinatori.fi/jobpostingprovider/documentation/KIPA-search-jobpostings-fi.html); [Apify Työmarkkinatori scraper](https://apify.com/studio-amba/tyomarkkinatori-scraper).
- Duunitori, described as Finland's largest job search engine, has no official public developer API in search results. Third-party Apify actors scrape it, and one notes job details are exposed as Schema.org JobPosting JSON-LD — [Teamdash Duunitori integration](https://www.teamdash.com/integrations/duunitori-integration/); [Apify Duunitori scraper](https://apify.com/automation-lab/duunitori-jobs-scraper).
- Open-source Finland-specific job tools on GitHub are tiny and mostly dead: peetuskytta/Jobdb-XYZ (7 stars), aapopalkama/Duunitori_scraper (1 star, last updated 2024), shoutcape/Tech-Jobs-Finland (1 star), and Virtual-Finland-Development/JobsInFinland.Api.Productizer (archived) — [GitHub search](https://github.com/search?q=duunitori+OR+tyomarkkinatori&type=repositories).
- openings-mcp covers Teamtailor, Recruitee, SmartRecruiters, Workable and other multi-country ATS through public endpoints, but names only Taiwan, Denmark, Japan, and China as country-specific boards — [openings-mcp README](https://github.com/amikai/openings-mcp).
- ai-job-search's `/add-portal` "investigates the portal (search URL pattern, result structure, access rules)" and scaffolds a CLI skill for any local board — [ai-job-search README](https://github.com/ai-job-search-dev/ai-job-search). career-ops has `providers/ADDING_A_PROVIDER.md` and a `discover` mode that turns company names into ATS boards in `portals.yml` — [career-ops AGENTS.md](https://github.com/career-ops-hq/career-ops/blob/main/AGENTS.md).
- swissdevjobs-cli (a Claude Code plugin and MCP) covers CH, DE, UK, US, CA, NL, and FR, **not Finland** — [swissdevjobs-cli](https://github.com/Stupidoodle/swissdevjobs-cli).

### Inferences
- The most practical Finland fill-in for a cloud-only user has three parts:
  1. Use career-ops' `discover` mode to add Finnish tech employers' Teamtailor/Recruitee/Greenhouse/Workable boards to `portals.yml`.
  2. Add JobSpy (Indeed `country_indeed="finland"` plus LinkedIn `location="Finland"`) as a supplementary source, accepting the ToS caveats.
  3. Paste Duunitori or LinkedIn JD text manually, rather than scraping Duunitori.
- A Työmarkkinatori provider would be the cleanest official source, but only if API access is granted. It is worth checking before writing a scraper.
- ai-job-search's generator-style `/add-portal` is a nicer extension mechanism than hand-writing a provider, but switching frameworks just for that is probably not worth it, since career-ops already documents adding providers.

### Gaps
- Not verified: whether The Hub (thehub.io, covered by career-ops' `thehub` provider) includes Finnish startup listings, and which Finnish tech employers use which ATS.
- Työmarkkinatori API access terms for private individuals were not confirmed.
- Whether Finnish-language CV conventions (e.g., photo, Finnish/English versions) are handled by any tool was not researched.
