# Enhancv Developer API: capabilities, cost/limits, and integration with Claude Code (web) and career-ops

Research date: 2026-10-22. All developer-doc pages were downloaded directly as server-rendered HTML (Docusaurus site, "Copyright © 2026 Enhancv"), so the endpoint details below are read from the pages themselves, not from search snippets. The doc site has 13 pages, all listed in [sitemap.xml](https://developers.enhancv.com/sitemap.xml), and all 13 were read.

## 1. What endpoints and capabilities exist (and which are missing)

### Takeaway
The Enhancv API is a small resume-storage-and-render API. It has six documented endpoints: list, create (from structured JSON), retrieve, export to PDF, delete, and upload/parse a PDF/DOC/DOCX. It has no update endpoint, no cover letters, no ATS check or scoring, no JD tailoring, no translation, no published OpenAPI spec, and no documented LinkedIn-import endpoint. All of the "AI" features (tailoring, ATS checker, bullet generator, translation) exist only in the consumer web app.

### Cited Findings
**Basics**
- Base URL `https://api.enhancv.com/api/v1`. Auth is a Bearer token in the `Authorization` header. Keys start with `enh_live_`, are generated under Account Settings → Profile → API Keys, and are "only shown once". — [Getting Started](https://developers.enhancv.com/); [Authentication](https://developers.enhancv.com/authentication/)
- The docs recommend storing keys in environment variables and warn "Don't expose keys in client-side code" and "Don't log API keys". — [Authentication](https://developers.enhancv.com/authentication/)

**Endpoints (method and path exactly as documented)**
- `GET /api/v1/resumes`: paginated list. Query parameters are `cursor` and `limit` (default 20, max 100). Returns `{resumes:[{id,title,filename,createdAt,updatedAt}], pagination:{cursor,limit}}`, sorted by ID oldest-first. — [List Resumes](https://developers.enhancv.com/api/resumes/)
- `POST /api/v1/resumes`: "Create a new resume from structured data… in the Enhancv analyzer format". `header` and `sections` are required; `title` and `style` are optional. Returns `201 Created {"id": ...}`. Created resumes are "marked as imported (`isImported: true`)". "Cover letters are not supported through this endpoint." "Resume limits depend on your subscription plan." — [Create Resume](https://developers.enhancv.com/api/create/)
- `GET /api/v1/resumes/:id`: returns the full resume in the same format Create accepts. "Only fields that are visible on the resume are returned", and hidden fields are omitted. "Cover letters are not accessible through this endpoint." — [Retrieve Resume](https://developers.enhancv.com/api/retrieve/)
- `GET /api/v1/resumes/:id/pdf`: returns raw `application/pdf` with `Content-Disposition: attachment; filename="John Doe.pdf"`. Rendering "typically takes 5-15 seconds", and the docs recommend a client timeout of at least 60 s. Returns 504 if generation times out. "The generated PDF includes accurate height calculations, so it matches the Enhancv editor output exactly." Results are "cached based on resume content". Page size follows the `isLetterSize` setting (US Letter or A4). — [Export Resume as PDF](https://developers.enhancv.com/api/export-pdf/)
- `DELETE /api/v1/resumes/:id`: deletes permanently and returns `{"success": true}`. — [Delete Resume](https://developers.enhancv.com/api/delete/)
- `POST /api/v1/resumes/upload`: multipart upload with a `file` field. Accepts PDF, DOC or DOCX up to 10 MB. Parsing uses "HRFlow AI", takes about 10-20 s in total, and returns `{"id": ...}`. "Original formatting is not preserved (Enhancv styling is applied)." "AI parsing may not be 100% accurate." Uploads "count toward your account's resume limit". — [Upload Resume](https://developers.enhancv.com/api/upload/)
- LinkedIn import has no endpoint. The page only says: "For LinkedIn URL parsing directly to Enhancv, please contact us. We'll walk you through the setup and enable it for your account." — [Import from LinkedIn](https://developers.enhancv.com/api/linkedin/)

**Data model**
- There are 26 section keys: `experiences, educations, industryExperiences (skills with level), summaries, volunteering, publications, projects, interests, findMeOnline, strengths, skills (title+description+tags), customs/customs2/customs3, achievements, awards, books, certificates, courses, languages, quotes, references, mytime, additionalExperiences, additionalPublications, additionalTechnologies`. The docs themselves say "27 types". — [Resume Structure Reference](https://developers.enhancv.com/api/resume-structure/)
- Every section needs a `column`: 0 = left, 1 = right, 2 = third column, which only works with `"multicolumn"`. `order` sets the order within a column. Months in `dateRange` are 0-based: "0=January, 11=December". — [Resume Structure Reference](https://developers.enhancv.com/api/resume-structure/)
- The header fields are `name, title, email, phone, location, website`. There are no LinkedIn or GitHub header fields; profile links go in the `findMeOnline` section, which takes icons. — [Resume Structure Reference](https://developers.enhancv.com/api/resume-structure/)
- `style.layout` takes 15 template values: `double` (Double Column), `ivyleague`, `elegant`, `newcondensed` (Modern), `polished`, `stockholm` (Contemporary), `double_colored` (Creative), `timeline`, `flipped_modern` (Stylish), `single` (Single Column), `condensed` (Compact), `multicolumn`, `classic`, `high_performer`, `minimal`. — [Create Resume](https://developers.enhancv.com/api/create/)
- Other `style` fields: two hex colors, `fontBody` (4 options: opensans/roboto/ptsans/interui), `fontHeading` (19 options), `fontSize` 0-4, `hideBranding` (boolean, "Hide Enhancv branding"), `isLetterSize` (A4 when false), and margin, line-height and column-layout options. — [Resume Structure Reference](https://developers.enhancv.com/api/resume-structure/)
- Field visibility is automatic: "Fields with empty strings, null, or undefined values are automatically hidden." — [Create Resume](https://developers.enhancv.com/api/create/)

**Spec, changelog and probing**
- No machine-readable spec is published. Direct requests on 2026-10-22 to `/openapi.json`, `/swagger.json`, `/llms.txt`, `/llms-full.txt` and `/robots.txt` all returned 404. — direct probe of [developers.enhancv.com](https://developers.enhancv.com/)
- The doc site has no changelog page (the sitemap lists none). — [sitemap.xml](https://developers.enhancv.com/sitemap.xml)
- A live unauthenticated probe from this cloud container on 2026-10-22 returned `HTTP/2 401 {"error":"Missing Authorization header","requestId":"req_…","status":401}` with headers `server: Heroku`, `via: … cloudfront.net (CloudFront)` and `x-api-version: 5.5.2`. A bogus key returned `401 {"error":"Invalid API key"}`. This matches the documented error shapes. — direct probe of `https://api.enhancv.com/api/v1/resumes`

**Undocumented hints**
- The Error Handling guide lists `400 "Invalid format. Must be 'pdf' or 'txt'"` for a `format` query parameter. No endpoint page documents that parameter, so a text export may exist but is undocumented. — [Error Handling](https://developers.enhancv.com/guides/errors/)
- The same guide lists `502 "Failed to fetch LinkedIn profile…"` from "an upstream provider (for example, the LinkedIn data provider)". — [Error Handling](https://developers.enhancv.com/guides/errors/)

**Consumer-app features (not in the API docs)**
- The pricing-page FAQ lists AI Resume Feedback with an "ATS score", "Resume Tailoring to Job Descriptions" with a match score and keyword recommendations, Resume Translation, a Bullet Point Generator and a Job Application Tracker. None of these appear anywhere in the developer docs. — [Enhancv pricing FAQ](https://enhancv.com/pricing/); compare [developers.enhancv.com](https://developers.enhancv.com/)

### Inferences
- "Updating a section" means `GET /resumes/:id`, editing the JSON, `POST /resumes` to create a new resume, then optionally `DELETE` the old one. Each edit therefore produces a new resume ID. The community MCP server documents the same pattern ("Enhancv has no update endpoint") ([kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv)).
- For an AI-assisted pipeline, the API is a rendering and storage backend. All intelligence (tailoring, keyword matching, ATS checks, cover letters) has to stay on the Claude/career-ops side.
- The Enhancv schema is richer in decorative sections (icons, `mytime` pie chart, `books`, `quotes`, skill `level` bars) than in ATS-relevant structure. A tailored-CV pipeline should only use `summaries`, `experiences`, `educations`, `projects`, `certificates`, `skills`/`additionalTechnologies` and `languages`.

### Gaps
- `txt` export: whether it works, and on which path, is not documented. I could not test it without a valid key.
- The skill `level` scale is inconsistent across the docs' own examples (`level: 5` in most, `level: 9` in the Resume Structure example). No range is documented.
- The docs claim "230+ icons". I did not verify the count, and it does not matter for this use case.
- LinkedIn import is handled by sales per account. The privacy policy names "Nubela (Proxycurl)" as the LinkedIn parsing provider ([Privacy](https://enhancv.com/privacy/)). I did not verify whether that provider is still operating.

## 2. Pricing, rate limits, quotas, terms of use and privacy (GDPR)

### Takeaway
API access requires the Business plan. The docs also call it "Business Plus" in one place. It starts at about $99/month, against about $13.32/month for consumer Pro. Rate limits are 60 requests/min, 1,000/hour and 10,000/day per key, far more than one person needs. The binding constraint is a possible per-plan resume cap: the docs' own error example says "Your plan allows 5 resumes". Enhancv R&D is a Bulgarian (EU) company, so GDPR applies, but its servers are in the US and resume data flows to OpenAI and HrFlow.ai as sub-processors.

### Cited Findings
**Plan names and pricing**
- The docs name the required plan inconsistently. The overview says "An Enhancv Business Plan - API access is only available for business plan users" ([Getting Started](https://developers.enhancv.com/)). The authentication page says "The API Keys section is only available to users on the Enhancv Business Plus plan… contact sales to upgrade" ([Authentication](https://developers.enhancv.com/authentication/)). The 403 error body reads `"API access requires a business plan"` ([Error Handling](https://developers.enhancv.com/guides/errors/)).
- Enhancv's help center (Jan 26, 2026) compares the plans:
  - **Pro:** "Designed for Individuals", commercial use "Restricted by our Terms", 300 resumes and cover letters, single user, "Starting from $13.32/m".
  - **Business:** "Teams & Organizations", commercial use allowed, unlimited resumes and cover letters, custom templates and branding, unlimited users, "Starting from $99/m".
  - "Prices are shown in local currency in some regions."
  - The article does not mention the API.
  — [Help: Pro vs Business](https://help.enhancv.com/en/articles/11588544-what-is-the-difference-between-enhancv-pro-and-enhancv-business)
- The enhancv.com/pricing page renders prices client-side. The static HTML shows "€ NaN" placeholders, so I could not read actual EUR prices from it. — [Enhancv pricing](https://enhancv.com/pricing/)

**Resume limits (conflicting)**
- The Create endpoint's example 403 reads `"Maximum resume limit reached. Your plan allows 5 resumes"` ([Create Resume](https://developers.enhancv.com/api/create/)). This contradicts "Unlimited" resumes for Business in the [help center](https://help.enhancv.com/en/articles/11588544-what-is-the-difference-between-enhancv-pro-and-enhancv-business). The example may be illustrative only.

**Rate limits**
- For the Business plan: 60 requests/minute, 1,000/hour, 10,000/day, applied per API key. Headers `X-RateLimit-Limit/Remaining/Reset` and `X-Request-Id` are returned. A 429 body includes `retryAfter` in seconds. Higher limits are available on request. — [Rate Limits](https://developers.enhancv.com/guides/rate-limits/)
- Docs inconsistency: the guide's sample retry code reads a `Retry-After` header, while the documented 429 body carries `retryAfter`. The community MCP author flags the same mismatch. — [Rate Limits](https://developers.enhancv.com/guides/rate-limits/); [kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv)

**Terms of service**
- "Enhancv is designed exclusively for individual job seekers. Commercial use of our platform is prohibited. Businesses interested in utilizing Enhancv's services should contact us… to establish a business account." — [Terms](https://enhancv.com/terms/)
- Billing and refunds: prices may change on 30 days' notice. "Any monthly fees paid hereunder are non-refundable if you have used our services during that billing period. Quarterly and Semi-annual fees are eligible for a partial pro-rated refund." — [Terms](https://enhancv.com/terms/)
- Account termination: "Enhancv, in its sole discretion, has the right to terminate your account for any reason at any time… forfeiture… of all content in your account." — [Terms](https://enhancv.com/terms/)
- Governing law: "the laws of Bulgaria". — [Terms](https://enhancv.com/terms/)
- AI clause in the Terms: "We do not sell or share your personal data with AI model providers." — [Terms](https://enhancv.com/terms/)
- No API-specific terms exist. The developer site's footer links only to the general Terms and Privacy pages. — [developers.enhancv.com](https://developers.enhancv.com/)

**Privacy policy**
- The policy is from "Enhancv R&D… registered office at 9A Sinanishko ezero Str., Sofia 1680, Bulgaria" and was last updated July 23, 2024. It cites GDPR/UK GDPR legal bases. — [Privacy](https://enhancv.com/privacy/)
- International transfers: "Our servers are located in the United States". Transfers rely on the European Commission's Standard Contractual Clauses. — [Privacy](https://enhancv.com/privacy/)
- Named third parties: AWS and Heroku (cloud), MongoDB Atlas (storage), **OpenAI ("AI Technologies")**, **HrFlow.ai ("Resume Parsing")**, Nubela/Proxycurl (LinkedIn parsing), Google Analytics and Amplitude, Sentry and Microsoft Clarity, Customer.io/Mandrill/Intercom, Paddle/Braintree. — [Privacy](https://enhancv.com/privacy/)
- Retention: data is kept no longer than "the period of time in which users have an account". After account deletion "we may retain some information… to prevent fraud… comply with applicable legal requirements". — [Privacy](https://enhancv.com/privacy/)
- The live API probe showed `server: Heroku` behind CloudFront. — direct probe of `https://api.enhancv.com/api/v1/resumes`

### Inferences
- The Terms' statement "We do not sell or share your personal data with AI model providers" sits in tension with the privacy policy's listing of OpenAI as a third party under "AI Technologies". The likely reading is "processor, not sharing for their own use", but that is not stated. Resume content created via the API may therefore be processed by OpenAI, and uploads definitely go to HrFlow.ai. The community MCP README gives the same warning ([kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv)).
- For a Finland-based candidate, the controller is an EU entity, so GDPR rights (access, erasure, portability) can be exercised against a Bulgarian company, while storage is in the US under SCCs. For one's own CV this is a personal choice, not a compliance blocker. If the candidate ever pushed third parties' data (e.g. references' contact details), that would deserve more care.
- At personal scale (a few dozen tailored CVs, each create + export + delete = 3 calls), the rate limits are irrelevant. The resume cap, if real, is handled by deleting after export.
- On cost: the API path costs at least $99/month against $13.32/month for Pro. The only API-exclusive value is automation (programmatic create/export). Everything else, including the editor, templates, AI tailoring and the ATS checker, is in Pro.

### Gaps
- I found no public page that states the Business / Business Plus price for EUR/Finland, its exact resume cap, or whether "Business" and "Business Plus" are different tiers. The user should check their own billing page.
- There is no data processing agreement (DPA) or sub-processor list specific to API customers, and no data-region option (EU hosting).
- The privacy policy is dated July 2024 and predates the API docs (© 2026). It may not reflect API-era sub-processors.

## 3. Official MCP server, SDK, Claude integration and community integrations

### Takeaway
Enhancv publishes no SDK, no OpenAPI spec, no MCP server and no Claude or ChatGPT app. There is one community MCP server, `@kieksme/enhancv-mcp` v1.0.1 (GPL-3.0, created 2026-10-08, 0 stars). It wraps all six endpoints, supports Claude Code (stdio via npx, or plugin) and documents the API's quirks well, but it is two weeks old and unaffiliated.

### Cited Findings
- The developer docs mention no SDK or MCP server. The only code samples are curl, Node fetch/axios and Python `requests`. — [Getting Started](https://developers.enhancv.com/); [Complete Workflow Example](https://developers.enhancv.com/guides/complete-workflow/)
- A web search for an Enhancv MCP server or Claude/ChatGPT integration on 2026-10-22 returned nothing official. — WebSearch, "Enhancv MCP server Claude ChatGPT app integration" (no Enhancv results)
- GitHub repo search for "enhancv" returns about 30 repos. All but one are clones, student projects or LaTeX look-alikes (e.g. `danilotat/enhancv-latex`, "a LaTeX template… in the style of enhancv"). The one real integration is `kieksme/mcp-enhancv`. Code search for `"api.enhancv.com"` finds only 3 unrelated hits (domain lists). — [GitHub search: enhancv](https://github.com/search?q=enhancv&type=repositories); [kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv)

**The kieksme/mcp-enhancv server**
- Tools:
  - `enhancv_list_resumes`, `enhancv_find_resumes`, `enhancv_get_resume`
  - `enhancv_create_resume` (validated against the documented structure)
  - `enhancv_upload_resume`, `enhancv_duplicate_resume` (retrieve + create)
  - `enhancv_export_resume_pdf`
  - `enhancv_delete_resume` (requires `confirm: true`)
  — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- Install for Claude Code: `claude mcp add enhancv-mcp -e ENHANCV_API_KEY=… -- npx -y @kieksme/enhancv-mcp`, or as a Claude Code plugin. — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- The README says claude.ai custom connectors are "not supported out of the box" because its HTTP transport needs a static bearer token and those products expect OAuth. — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- Deliberately not implemented: LinkedIn import, TXT export and cover letters, "intentionally absent rather than guessed". — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- Behaviour: it retries on 429 using `retryAfter`, never retries POST or DELETE after a 5xx (to avoid duplicates), and has file access off unless `ENHANCV_FILES_DIR` is set. — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- Its documentation-inconsistency notes match mine: 27 vs 26 sections, "business plan" vs "Business Plus", and `Retry-After` vs `retryAfter`. — [kieksme/mcp-enhancv README](https://github.com/kieksme/mcp-enhancv)
- npm package `@kieksme/enhancv-mcp`: version 1.0.1, created 2026-10-08, license GPL-3.0-or-later. It is reachable from this cloud container: `npm view` succeeded through the proxy on 2026-10-22. — [npm](https://www.npmjs.com/package/@kieksme/enhancv-mcp)
- GitHub metadata on 2026-10-22: 0 stars, 0 forks, 8 open issues, last updated 2026-10-21. — [kieksme/mcp-enhancv](https://github.com/kieksme/mcp-enhancv)

### Inferences
- In a Claude Code on the web session, the lowest-risk integration is plain `curl` with `$ENHANCV_API_KEY` from the environment settings, since the API is only six REST calls. The MCP server adds convenience (schema validation, retries) but gives a 2-week-old, 0-star third-party package access to the key and resume data. If it is used, pin the version and review the code first.
- The MCP's documented quirks are a useful independent cross-check that my reading of the docs is accurate.

### Gaps
- I did not verify whether Claude Code on the web sessions load a project `.mcp.json` stdio server (`npx …`) automatically. This should be confirmed in the user's environment.
- I did not read the MCP's source code or its 8 open issues; the GitHub issues API was not reachable from this session.

## 4. ATS performance of Enhancv PDFs, especially for Nordic ATS (Teamtailor, Workday, SmartRecruiters, Recruitee)

### Takeaway
Evidence is thin and mostly conflicted. Enhancv's own tests claim two-column templates parse as well as single-column ones. The only detailed third-party test, by a competitor, found the Double Column template parsed cleanly on only 1 of 5 major ATS, while single-column "Traditional" passed 5/5. A second competitor's October 2026 re-test found both single- and double-column read in correct order. I found no test at all on Teamtailor, Recruitee or SmartRecruiters, the ATS most common in Finland. The safe choice via the API is `layout: "single"` / `"classic"` / `"ivyleague"` with no icons and no skill-level bars.

### Cited Findings
**Enhancv's own claims**
- "96.73% — Enhancv's average ATS parse score in our testing." Two-column versus single-column: "98% vs 95%". "All of our templates are ATS-friendly, two-column ones included." Their suggested self-test is to paste the PDF into a plain-text editor. — [Enhancv blog (self-published)](https://enhancv.com/blog/is-enhancv-ats-friendly/)
- The pricing FAQ says exports have "a full text layer, not rasterized images", decorative icons are "visual elements only", "Only one legacy template uses a minimal table structure", and section titles "match parser dictionaries used by Sovren and RChilli". — [Enhancv pricing FAQ](https://enhancv.com/pricing/)

**Resume Optimizer Pro (competitor; the author concedes "take that with salt"; published April 22, 2026)**
- Setup: 5 Enhancv templates × 5 parsers (Workday, Greenhouse, Lever, iCIMS, Taleo), one fictional marketing-manager resume, single run, graded on 5 fields.

| Template | Clean parses (of 5) |
|---|---|
| Double Column | 1 |
| Modern | 2 |
| Timeline | 0 |
| Traditional | 5 |
| Elegant | 4 |

- Failures reported:
  - Workday: sidebar skills came out empty for Double Column.
  - iCIMS: contact icons polluted the email field.
  - Timeline: dates were lost to the graphic.
  — [Resume Optimizer Pro vs Enhancv](https://resumeoptimizerpro.com/blog/resume-optimizer-pro-vs-enhancv)

**ATS Verification (competitor selling a $5 rebuild)**
- "In our October 2026 re-test, a single-column and a double-column Enhancv template (files supplied by Enhancv) both read in the correct order. Templates with skill bars or charts were not tested." No per-ATS results are given. — [ATS Verification vs Enhancv](https://atsverification.com/vs/enhancv/)
- Conflict: a search-engine summary attributed a claim of "30 to 45%" failure on Workday/Taleo to this site. That text is not on the current page, so it may come from an earlier version. Treat it as unverified. — [ATS Verification vs Enhancv](https://atsverification.com/vs/enhancv/)

**OwlApply (sells its own builder/checker; updated Oct 19, 2026)**
- "the single-column templates parse well; the two-column designs depend on how the PDF's reading order is generated". Its own parser data flags "two-column 17.2% of files, icons 10.6%". — [OwlApply Enhancv review](https://owlapply.com/en/blog/enhancv-review)

**Nordic ATS**
- Teamtailor: Teamtailor's product news describes an updated parser with a preview/edit step before a candidate is added. I saw this only as a search snippet and did not open the page; it says nothing about columns. — [Teamtailor product news](https://www.teamtailor.com/en/productnews/parse-candidates-faster-and-easier/)
- A third-party guide (HireFlow, Aug 2026, unverified, search snippet only) lists "tables, text boxes, or columns" as common causes of Teamtailor upload problems. — [HireFlow](https://hireflow.net/blog/teamtailor-resume-upload-issues-us-formatting-guide)

### Inferences
- All three outside sources are competitors, and the only source claiming two-column templates are fully safe is Enhancv itself. The consistent signal across all of them is that single-column Enhancv templates are safe, while two-column, timeline, icon and graphic-skill templates are the risk.
- Via the API this risk is controllable:
  - Choose `layout: "single"` (or `classic`/`ivyleague`/`minimal`, which are probably single-column but not verified).
  - Put all sections in `column: 0`.
  - Avoid `findMeOnline` icons, `industryExperiences` levels, `mytime` and `timeline`.
  - Use `skills`/`additionalTechnologies` with tags.
- The ROP "Traditional" template has no API value of that name. The mapping to `classic`, `single` or `ivyleague` is unknown.
- career-ops already runs a deterministic ATS scorer (`verify-ats.mjs`) on its own HTML. No equivalent exists for Enhancv output. A `pdftotext` reading-order check of the Enhancv PDF would be needed to get parity.

### Gaps
- I found no independent test of Enhancv PDFs on Teamtailor, Recruitee, SmartRecruiters or Workday's Nordic tenants. No Reddit thread with parse evidence was found in the time available.
- I could not map the reviewers' template names to API `layout` values with certainty.

## 5. Concrete integration options with Claude Code on the web and career-ops: what is gained and what is lost

### Takeaway
Integration is technically straightforward from a cloud session. `api.enhancv.com` is reachable through the proxy, and the key can live in an environment variable. The sensible design is complement, not replace: career-ops keeps the tailoring, fact gates and JSON payload, then a small mapper pushes that payload to `POST /resumes` with an ATS-safe single-column A4 style, exports the PDF, and deletes the resume. The cost is that career-ops's render-time guards no longer see the final artifact, so the Enhancv PDF must be re-checked by text extraction.

### Cited Findings
**What career-ops already does (local checkout at commit `dff9703`, 2026-10-21)**
- `build-cv-html.mjs` is a "Deterministic HTML CV renderer": "The agent reads cv.md + config/profile.yml, tailors the content, and writes a compact JSON payload". — `/home/user/career-ops/build-cv-html.mjs`
- `generate-pdf.mjs` renders "HTML → PDF via Playwright".
  - Options: `--format=letter|a4`, `--max-pages`, `--skip-fact-check`.
  - It fails generation when section order diverges from cv.md (unless `--allow-reorder`) or when experience is not newest-first (unless `--allow-nonchronological`).
  - It calls `verify-cv-facts.mjs` `assertFacts(html)` on the HTML before rendering.
  — `/home/user/career-ops/generate-pdf.mjs` (lines 1-40, 1526-1552)
- `verify-cv-facts.mjs` accepts `<generated-cv.html|md|tex>`, so plain text or markdown extracted from a third-party PDF can also be gated. — `/home/user/career-ops/verify-cv-facts.mjs`
- `verify-ats.mjs` is a deterministic 0-100 ATS score that reads "one CV HTML (the output of `pdf` mode, before PDF rendering)". — `/home/user/career-ops/verify-ats.mjs`
- `modes/pdf.md` already runs checks on the JSON payload before rendering: Step 17a `cv-title-check.mjs` and Step 17b `verify-cv-structure.mjs`. — `/home/user/career-ops/modes/pdf.md`
- `modes/pdf.md` already has an optional external-renderer path (Canva) and an opt-in `--ats` single-column variant (`templates/ats/cv-template.ats.html`). — `/home/user/career-ops/modes/pdf.md`
- The career-ops payload fields are `candidate{name,title,phone,email,linkedin,github,portfolio,location,photo}`, `summary`, `competencies[]`, `experience[{company,role,location,context,dates,bullets}]`, `projects[{name,url,badge,tech,description}]`, `education[{title,org,location,year,description}]`, `certifications`, `awards` and `skills[{category,items}]`. — `/home/user/career-ops/modes/pdf.md` (JSON Input Schema)

**Enhancv side**
- Reachability: an unauthenticated request from this cloud container returned the documented 401 JSON, so outbound HTTPS to the API works through the proxy. — direct probe of `https://api.enhancv.com/api/v1/resumes`
- Documented end-to-end flow: create → `GET /resumes/{id}/pdf` → write file. — [Export Resume as PDF](https://developers.enhancv.com/api/export-pdf/)
- A4 is the default when `isLetterSize: false`, and `hideBranding: true` hides Enhancv branding. — [Resume Structure Reference](https://developers.enhancv.com/api/resume-structure/)

### Inferences

**Option A (recommended if the API is used at all): career-ops tailors and gates, Enhancv renders.**
1. Run career-ops `pdf` mode through the payload and the existing gates (17a/17b, `build-cv-html` + `verify-cv-facts` on the HTML).
2. A small mapper script converts the payload to Enhancv format:
   - `candidate` → `header` (portfolio → `website`; LinkedIn/GitHub need a plain-text `customs` line or `findMeOnline` without icons).
   - `summary` → `summaries`.
   - `experience` → `experiences`. Parse "June 2022 - Present" into a 0-based `dateRange` with `isOngoing`. The `context` line maps to `description`.
   - `education.year` → `dateRange.toYear`.
   - `certifications` → `certificates`, `awards` → `awards`.
   - `skills` and `competencies` → `skills` (title + tags).
   - Style: `{layout:"single", isLetterSize:false, hideBranding:true}`, everything in `column: 0`.
3. Call the API with three curl commands: `POST /resumes`, `GET /resumes/{id}/pdf -o output/…pdf`, `DELETE /resumes/{id}`.
4. Re-gate the result: run `pdftotext` on the Enhancv PDF, then `verify-cv-facts.mjs` on the `.md`, plus a manual reading-order check.

What Option A gains and loses:
- **Gains:** Enhancv's typography and the option to open the same resume in Enhancv's visual editor for manual polish before export.
- **Loses:**
  - career-ops's render-time guarantees: section-order and chronology guards, `--max-pages`, and the `verify-ats.mjs` score all run on career-ops HTML, not on Enhancv's render.
  - Exact control over line breaks and page count.
  - Zero-network rendering: data now goes to Enhancv, US servers and sub-processors.
  - Some fields: the photo, link display text, and `badge`/`tech` on projects unless folded into the description.
  - Each run costs about 3 API calls and 10-20 s of latency, which is negligible.

**Option B: community MCP server.** The same flow, driven by MCP tools instead of curl. It is convenient for interactive "show me / duplicate / export" requests but adds a supply-chain dependency (see section 3).

**Option C: use upload to bootstrap, not to tailor.** Upload an existing CV (PDF/DOCX), then `GET /resumes/:id` to obtain structured JSON. This can help draft `cv.md` during onboarding. But HrFlow parsing "may not be 100% accurate", so under career-ops's Source-of-Truth rules any output must be confirmed by the user, as in `intake` mode. Do not use upload in the tailoring loop: it reintroduces AI parse errors after the fact gate has passed.

**Option D: editor handoff.** Create the tailored resume via the API, let the user tweak it visually in Enhancv's web app, then use `GET /resumes/:id` to pull the final JSON back and diff it against `cv.md` and the gated payload, so any manual edits that introduce unsupported claims are caught.

**Replace vs complement.** Replacing career-ops's PDF generation would discard its fact, structure and ATS gates in exchange for templates. career-ops already ships 7+ HTML templates (`templates/cv-template*.html`, plus an ATS template) and a LaTeX path, and for a software engineer in Finland the plain single-column output is arguably the ATS-safer artifact. Enhancv is best treated as an optional "styled variant" renderer, the same way `pdf.md` treats Canva.

**Language and market.** The API has no translation or locale features (it has `isLetterSize` only). Finnish- or Swedish-language CVs would be translated by Claude and then pushed as text. The fonts listed are Latin-script fonts; å, ä and ö support was not verified.

### Gaps
- I could not run an authenticated create/export round-trip, because no Enhancv key was present in this container's environment. Actual PDF text-layer quality, reading order of the `single` layout, A4 output and the real resume cap remain untested. The first test should be: create one resume, export it, run `pdftotext -layout`, then delete it.
- Whether `hideBranding: true` is honoured on the user's plan is not documented per plan.

## 6. Is the API usable for one person's own job search (not just for building SaaS)?

### Takeaway
Yes, technically and contractually. The API is scoped to the key-holder's own account, and the Business plan it requires explicitly permits commercial use, so there is no "SaaS only" restriction. Economically, though, it is a $99+/month plan buying automation that the consumer Pro plan ($13.32+/month) and career-ops's free local renderer largely already cover.

### Cited Findings
- Every endpoint operates on "your account": "Retrieve a paginated list of all resumes in your account", "Resume not found or doesn't belong to your account". — [List Resumes](https://developers.enhancv.com/api/resumes/); [Retrieve Resume](https://developers.enhancv.com/api/retrieve/)
- Business plan: "Commercial use ✅ Allowed", "Starting from $99/m". Pro: commercial use "Restricted by our Terms", "Starting from $13.32/m". — [Help: Pro vs Business](https://help.enhancv.com/en/articles/11588544-what-is-the-difference-between-enhancv-pro-and-enhancv-business)
- The consumer Terms say "Enhancv is designed exclusively for individual job seekers", so personal job-search use is the platform's core intended use. — [Terms](https://enhancv.com/terms/)
- The docs warn "Don't reuse keys across multiple applications". — [Authentication](https://developers.enhancv.com/authentication/)
- I found no clause limiting API use to building products, and no API-specific terms. — [developers.enhancv.com](https://developers.enhancv.com/); [Terms](https://enhancv.com/terms/)

### Inferences
- For this user, who already pays for API access, the marginal cost of trying Option A is zero apart from the time to write a mapper of roughly 100-150 lines.
- If the subscription was bought only for this, the value case is weak. career-ops already produces fact-gated, ATS-scored A4 PDFs locally, and Enhancv's distinctive value (visual editor, AI tailoring, ATS checker) is in the web app, not the API.
- To keep the key safe in Claude Code on the web, set `ENHANCV_API_KEY` in the environment's secrets/env settings. Never write it into career-ops files: the repo's `.env` handling is for `CAREER_OPS_*` variables, and `data/` is user-layer but may be committed in a fork.

### Gaps
- The user's exact plan name, price, resume cap and whether "developer subscription" equals "Business" or "Business Plus" are unknown. They should check app.enhancv.com → Billing.
