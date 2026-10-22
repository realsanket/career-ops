# Finnish software job market (2026): channels, ATS platforms, conventions and constraints, and what job tools must cover

Research date: 2026-10-22. Method: web search/fetch plus live, read-only probes of public ATS APIs and careers pages (curl/node from this session, 2026-10-22), plus reading the local career-ops checkout at `/home/user/career-ops` (commit `dff9703`, 2026-10-21). Where a figure comes from a live probe, the probed URL is cited and counts are as of 2026-10-22. Where a figure was only seen in a search-result summary (not on a page I could open), it is marked "(search summary, unverified)".

## Q1. Main job channels for software roles in Finland, their importance, and machine access (API / RSS / scraping terms)

### Takeaway
For software roles, the channels that matter are employer ATS boards (reached through company career pages), LinkedIn, Duunitori, Job Market Finland (Työmarkkinatori), The Hub for startups, agencies, and networking. Networking matters because Finnish sources agree that most jobs are never advertised. Oikotie Työpaikat has closed. Of the boards, only The Hub has an open JSON API that a tool can use. Duunitori's robots.txt and terms forbid scraping. Työmarkkinatori's search API needs credentials and IP allowlisting from KEHA-keskus. Jobly and LinkedIn have no open API.

### Cited Findings

**Overview lists**
- TEK (the Finnish union of tech graduates) lists the most common recruitment platforms in Finland under these headings:
  - Job boards: Job Market Finland (Työmarkkinatori), Duunitori.fi, Jobly.fi and LinkedIn Jobs.
  - "Jobs in English": Jobs in Helsinki, Careerjet, Work in Finland and Jobsportal.
  - Public sector: Kuntarekry, Valtiolle and Seure.
  - Agencies that suit tech candidates: Academic Work, Experis, Finitec, Games Jobs Finland, Nico, Qasvu, Talented ("experienced developers"), WiseIT and Barona.
  - TEK also states that "only 20-30 % of available jobs are made public."
  - Source: [TEK – Where to look for a job in Finland](https://www.tek.fi/en/services-and-benefits/job-search-and-career/tools-and-information-for-job-seekers/where-to-look-for-a-job-in-finland)
- Survey data on the hidden job market:
  - A YTK unemployment-fund survey of 18,562 members found that 68% said their most recent job was a "hidden job". Personal networks were the most common route (29%). This is a self-selected member survey. — [Verkkouutiset](https://www.verkkouutiset.fi/a/tyopaikoista-yli-kaksi-kolmasosaa-on-piilotyopaikkoja/) (search summary; article date not confirmed)
  - Työmarkkinatori published hidden-job search tips on 2026-04-08. — [Työmarkkinatori news](https://tyomarkkinatori.fi/en/news/2026_4_8_vinkkeja_piilotyopaikkojen_etsintaan)
- InfoFinland (official) advises open applications and calling the employer before applying. It also says to put your LinkedIn profile on your CV. — [InfoFinland – Job application and CV](https://infofinland.fi/work-and-enterprise/find-a-job-in-finland/job-application-and-cv)

**Duunitori**
- Reach and volume:
  - Duunitori calls itself Finland's most popular job search service.
  - Its own 2025 figures: more than 300,000 job ads published, about 24% fewer than in 2024; more than 120 million ad views, up about 32%. These are company-reported. — [Duunitori – luetuimmat työpaikkailmoitukset 2025](https://duunitori.fi/tyoelama/luetuimmat-tyopaikkailmoitukset-2025)
  - Its employer page claims "over 5 million visits per month". — [Duunitori – recruitment in English](https://duunitori.fi/rekrytointi/in-english) (search-result title, not opened)
- Machine access:
  - Its robots.txt has `User-agent: * / Disallow: /`, with exceptions only for named crawlers, and also disallows `/api/` (fetched 2026-10-22). — [duunitori.fi/robots.txt](https://duunitori.fi/robots.txt)
  - Its terms of use forbid scraping: "Käyttäjä ei saa tallentaa, arkistoida, skrapata tai muutoin järjestelmällisesti kopioida Palvelun sisältöä…" ("The user may not store, archive, scrape or otherwise systematically copy the Service's content…"). — [Duunitori Group terms of use](https://duunitori.fi/compliance/kayttoehdot)
  - No official public API or RSS feed was found. Third-party Apify scrapers exist and parse the HTML and Schema.org JobPosting JSON-LD. — [Apify duunitori scraper](https://apify.com/automation-lab/duunitori-jobs-scraper.md); [Apify unfenced-group](https://apify.com/unfenced-group/duunitori-fi-scraper)
  - It offers e-mail job alerts ("Duunivahti"). — [duunitori.fi/duunivahti](https://duunitori.fi/duunivahti)
- Free employer ads stay up at most 14 days. — [Duunitori help](https://help.duunitori.fi/fi/articles/9748796-employer-how-to-post-a-job-ad) (search summary)

**Job Market Finland (Työmarkkinatori, the public employment service)**
- Search API:
  - A job-posting search API exists: `https://api.ahtp.fi/kipa/p67/v2/jobpostings`. It takes POST requests and returns NDJSON, with code values from Työmarkkinatori's codelists.
  - Access needs a `KIPA-Subscription-Key`. KEHA-keskus issues the credentials and the IP allowlisting.
  - The documentation's first version is dated 10.3.2026. It states no rate limits or licence.
  - Source: [KIPA search-API documentation](https://tyomarkkinatori.fi/jobpostingprovider/documentation/KIPA-search-jobpostings-fi.html)
- A separate management (write) API lets external services publish postings for employers. — [KIPA manage-jobpostings doc](https://tyomarkkinatori.fi/jobposting-new/documentation/KIPA-manage-jobpostings-fi.html)
- Its robots.txt disallows `/api/` and `/*/api/`. — [tyomarkkinatori.fi/robots.txt](https://tyomarkkinatori.fi/robots.txt)
- Third-party Apify scrapers exist. — [Apify tyomarkkinatori scraper](https://apify.com/studio-amba/tyomarkkinatori-scraper)

**Work in Finland** (government, part of Talent Boost)
- Its "Open jobs" page listed 915 English-speaking jobs when fetched. The same page tells users to create a Job Market Finland applicant profile.
- Source: [workinfinland.com/en/open-jobs](https://www.workinfinland.com/en/open-jobs/); [Work in Finland home](https://www.workinfinland.com/en/)

**Oikotie Työpaikat**
- It has closed. The site reads "Oikotie Työpaikat on sulkeutunut" ("Oikotie Työpaikat has closed") (fetched 2026-10-22). — [tyopaikat.oikotie.fi](https://tyopaikat.oikotie.fi/)
- One secondary source dates the closure to February 2025. — [JobCrawls – Best job websites Finland 2026](https://jobcrawls.com/en/resources/jobs-in-finland/best-job-websites-finland)

**Jobly**
- TEK lists it.
- robots.txt sets `Crawl-delay: 10` (fetched). — [jobly.fi/robots.txt](https://jobly.fi/robots.txt)
- The homepage returned HTTP 403 to a scripted request. No API was found.

**The Hub (Nordic startups)**
- It has a public JSON endpoint, `https://thehub.io/api/v2/jobsandfeatured`.
- A probe with `countryCode=FI` on 2026-10-22 returned 182 Finnish postings over 13 pages, from employers such as Measurlabs, Verda, ICEYE, Hunome and Hoxhunt. — [The Hub API (FI)](https://thehub.io/api/v2/jobsandfeatured?countryCode=FI&page=1)
- Its robots.txt disallows only `/startups/joblistwidget/`. — [thehub.io/robots.txt](https://thehub.io/robots.txt)

**LinkedIn**
- A 2019 Finnish thesis (19 recruiters) found that recruiters in Finland preferred LinkedIn and that most hired through it. The sample is small and old. — [Theseus thesis](https://www.theseus.fi/handle/10024/265441)
- No 2025–2026 Finland-specific statistic on LinkedIn's share as a channel was found.

**Talented**
- It is a developer-recruitment agency, part of the "Talented Family" of companies in Norway and Finland. The size figures are from about 2020. — [The Hub listing](https://thehub.io/jobs/60226076759e3670693c6e00) (search summary)

### Inferences
- The best automated coverage comes from reading employer ATS APIs directly, plus The Hub. Duunitori and Työmarkkinatori hold most of the Finnish-language, SME and public-sector volume. A compliant tool cannot ingest them freely.
  - Duunitori: terms and robots.txt both prohibit it.
  - Työmarkkinatori: the API needs an onboarding agreement.
  - The realistic route for a single user is each site's own e-mail alerts (Duunivahti, Työmarkkinatori saved searches), forwarded into Gmail and parsed by the assistant. This is untested.
- Because TEK says only 20–30% of jobs are public, a Finland-focused assistant should support networking workflows: contact lookup, warm-intro mapping and open applications. Scanning alone is not enough.

### Gaps
- No independent market-share or traffic data comparing Duunitori, Jobly, Työmarkkinatori and LinkedIn for IT jobs in 2025–2026.
- I could not confirm whether Työmarkkinatori's search API is available to private individuals or only to organisations, or what its licence terms are. The onboarding page was not read.
- No public statistic on the share of English-language IT job ads in Finland.
- Jobly's ownership and terms were not verified, because the homepage returned 403.

## Q2. Which ATS platforms Finnish tech employers use, and how that compares with career-ops providers

### Takeaway
Finnish tech employers mostly run mainstream ATSs that career-ops already reads:
- Greenhouse: Wolt, Smartly.io, Oura, Solita, RELEX, Yousician
- Ashby: Supercell, Reaktor, ICEYE
- Teamtailor: Futurice, Vincit, Siili, Eficode, Columbia Road, Netum, Qvik — popular with Finnish consultancies
- Workday: KONE, Fiskars, Unity
- SAP SuccessFactors: Fortum, Wärtsilä, Vaisala, probably Nordea
- Oracle Recruiting Cloud: Nokia
- SmartRecruiters: Tieto(evry)
- Workable: Varjo

career-ops ships none of these Finnish employers as scanner entries. Its only Finnish entry is Aiven, scanned by web search. It also has no provider for Finnish or Nordic boards and ATSs: Duunitori, Työmarkkinatori, Jobly, Laura, HR-manager/Talentadore, Jobylon, Varbi.

### Cited Findings

**Employer → ATS evidence** (live probes, 2026-10-22; "FI" = postings whose location names a Finnish city or Finland)

| Employer | ATS (evidence) | Postings (total / FI) | career-ops support |
|---|---|---|---|
| Wolt | Greenhouse `wolt` — [boards-api.greenhouse.io/v1/boards/wolt/jobs](https://boards-api.greenhouse.io/v1/boards/wolt/jobs). careers.wolt.com is a custom front end. | 200 / 21 (Helsinki) | greenhouse provider |
| Supercell | Ashby `supercell` — [api.ashbyhq.com/posting-api/job-board/supercell](https://api.ashbyhq.com/posting-api/job-board/supercell) | 39 / 29 (one is an "Unlisted TEST job") | ashby provider |
| Reaktor | Ashby `reaktor` — [api.ashbyhq.com/…/reaktor](https://api.ashbyhq.com/posting-api/job-board/reaktor) | 19 / 15 (Helsinki, Turku) | ashby |
| ICEYE | Ashby `iceye` — [api.ashbyhq.com/…/iceye](https://api.ashbyhq.com/posting-api/job-board/iceye) | 194 / 93 (Espoo) | ashby |
| Smartly.io | Greenhouse `smartlyio`; careers page links job-boards.greenhouse.io/smartlyio — [smartly.io/careers](https://www.smartly.io/careers), [API](https://boards-api.greenhouse.io/v1/boards/smartlyio/jobs) | 58 / 20 | greenhouse |
| Oura | Greenhouse `oura`; careers page references job-boards.greenhouse.io/oura — [ouraring.com/careers](https://ouraring.com/careers), [API](https://boards-api.greenhouse.io/v1/boards/oura/jobs) | 81 / 4 (Helsinki hybrid) | greenhouse |
| Solita | Greenhouse `solita` (slug found by probe; solita.fi returned 403) — [API](https://boards-api.greenhouse.io/v1/boards/solita/jobs) | 62 / 30 (Helsinki, Tampere, Turku, Oulu, Lahti) | greenhouse |
| RELEX Solutions | Greenhouse `relex` (slug found by probe; titles such as "Head of People Operations – EMEA @ Helsinki" match) — [API](https://boards-api.greenhouse.io/v1/boards/relex/jobs) | 41 / 7 | greenhouse |
| Yousician | Greenhouse `yousician` — [API](https://boards-api.greenhouse.io/v1/boards/yousician/jobs) | 2 / 2 | greenhouse |
| Aiven | Greenhouse. The careers page says recruiting e-mails come from @greenhouse.io or @eu.greenhouse.io. The slug was not found on boards-api, and job-boards.eu.greenhouse.io/aiven returned 404. — [aiven.io/careers](https://aiven.io/careers) | n/a | Template entry uses `scan_method: websearch` ([portals.example.yml](/home/user/career-ops/templates/portals.example.yml), around line 2720) |
| Futurice | Teamtailor on the branded domain careers.futurice.com (Teamtailor CDN assets; job links careers.futurice.com/jobs/…) — [futurice.com/careers/open-positions](https://www.futurice.com/careers/open-positions), [careers.futurice.com](https://careers.futurice.com/) | not counted | teamtailor provider; needs explicit `provider: teamtailor` because the domain is branded ([providers/teamtailor.mjs](/home/user/career-ops/providers/teamtailor.mjs)) |
| Vincit | Teamtailor `vincitoyj`; the careers page embeds the Teamtailor API — [vincit.com/careers](https://www.vincit.com/careers), [RSS](https://vincitoyj.teamtailor.com/jobs.rss) | 4 items | teamtailor |
| Siili Solutions | Teamtailor `siili` — [siili.com/join-us](https://www.siili.com/join-us), [RSS](https://siili.teamtailor.com/jobs.rss) | 6 items | teamtailor |
| Eficode / Columbia Road / Netum / Qvik | Teamtailor RSS feeds respond — [eficode](https://eficode.teamtailor.com/jobs.rss), [columbiaroad](https://columbiaroad.teamtailor.com/jobs.rss), [netum](https://netum.teamtailor.com/jobs.rss), [qvik](https://qvik.teamtailor.com/jobs.rss) | 7 / 6 / 3 / 2 items | teamtailor |
| Nitor | No ATS found. Postings are CMS pages at nitor.com/en/careers/<slug>. — [nitor.com/en/careers](https://nitor.com/en/careers) | n/a | websearch or manual only |
| Nokia | Oracle Recruiting Cloud. jobs.nokia.com redirects to /en/sites/CX_1 and loads from fa-evmr-saasfaprod1.fa.ocs.oraclecloud.com. — [jobs.nokia.com](https://jobs.nokia.com) | not counted | oraclecloud provider |
| KONE | Workday — [kone.wd3.myworkdayjobs.com/en-US/Careers](https://kone.wd3.myworkdayjobs.com/en-US/Careers), linked from [kone.com careers](https://www.kone.com/en/careers/) | not counted | workday provider |
| Fiskars | Workday — [fiskars.wd3.myworkdayjobs.com/FiskarsGroup](https://fiskars.wd3.myworkdayjobs.com/en-US/FiskarsGroup), linked from [fiskarsgroup.com/careers](https://www.fiskarsgroup.com/careers/) (Espoo postings seen) | not counted | workday |
| Unity | Workday — [unitytech.wd1.myworkdayjobs.com/Unity](https://unitytech.wd1.myworkdayjobs.com/Unity), linked from [unity.com/careers/positions](https://unity.com/careers/positions). Helsinki postings not checked. | not counted | workday |
| Fortum | SAP SuccessFactors RMK (rmkcdn.successfactors.com assets) — [jobs.fortum.com](https://jobs.fortum.com/) | not counted | successfactors provider (explicit `provider:` + `api:` for a branded host) |
| Wärtsilä | SuccessFactors — [careers.wartsila.com](https://careers.wartsila.com/), linked from [wartsila.com/careers](https://www.wartsila.com/careers) | not counted | successfactors |
| Vaisala | SuccessFactors RMK — [careers.vaisala.com](https://careers.vaisala.com/search) | not counted | successfactors |
| Nordea | Probably SuccessFactors RMK: posting URLs take the RMK shape careers.nordea.com/job/<title>/<id>, e.g. [this posting](https://careers.nordea.com/job/%C5%81%C3%B3d%C5%BA-People-Service-Assistant-in-Talent-Services-93-281/1154437901). **Unverified**: the connection was reset. | n/a | successfactors (if confirmed) |
| Tieto (Tietoevry) | SmartRecruiters `Tieto2`; careers.tieto.com links jobs.smartrecruiters.com/my-applications/Tieto2 — [careers.tieto.com](https://careers.tieto.com/), [API country=fi](https://api.smartrecruiters.com/v1/companies/Tieto2/postings?limit=100&country=fi) | 61 FI (Tampere, Jyväskylä, Espoo…) | smartrecruiters provider |
| Varjo | Workable (workable embed.js on varjo.com/jobs). Slug **unverified**: the Workable API was rate-limited (Cloudflare 1015). — [varjo.com/jobs](https://varjo.com/jobs) | n/a | workable provider |
| Rovio (Sega) | **Unknown.** Custom WordPress page with no ATS signature in its HTML. — [rovio.com/open-positions](https://www.rovio.com/open-positions/) | n/a | websearch or manual |
| Elisa, OP Financial Group, Telia Finland | **Not determined.** Pages are JS-rendered, guessed paths returned 404, and Elisa's recruitment page links to barona.fi/tyopaikat and clevry.com. — [elisa.fi rekrytointi](https://www.elisa.fi/yhtiotieto/rekrytointi/) | n/a | unknown |

**Probe caveats**
- SmartRecruiters' public API returns HTTP 200 with `totalFound: 0` for any slug, including nonexistent ones. That makes it a false-positive trap for auto-detection: a 200 is not evidence of a tenant. Seen across dozens of slugs, e.g. [api.smartrecruiters.com/v1/companies/supercell/postings](https://api.smartrecruiters.com/v1/companies/supercell/postings?limit=1).
- `<tenant>.rekrytointi.com` hosts (tested: elisa, op, telia) redirect to or show [laura.fi](https://laura.fi/), the Finnish ATS vendor Laura. So rekrytointi.com belongs to Laura's infrastructure, but these redirects do **not** prove that Elisa, OP or Telia use Laura.

**career-ops coverage** (local checkout)
- `providers/` contains about 120 provider modules. Relevant ones include greenhouse, ashby, lever, teamtailor, workday, successfactors, oraclecloud, smartrecruiters, workable, recruitee, personio, thehub and platsbanken (Sweden). There is **no** provider for duunitori, tyomarkkinatori, jobly, linkedin, indeed, laura, talentadore/hr-manager, jobylon, varbi or reachmee. — [/home/user/career-ops/providers/](/home/user/career-ops/providers/)
- In `templates/portals.example.yml`:
  - The only Finland-based company is Aiven, via websearch. The Nordic sections list Stockholm and Copenhagen companies, none Finnish.
  - The Hub is present only as a commented-out example, with default `countryCode: EU`.
  - Source: [/home/user/career-ops/templates/portals.example.yml](/home/user/career-ops/templates/portals.example.yml) (lines ~1660, ~2645–2790, ~2720)
- The Hub provider requires `countryCode` on every request, because omitting it scopes results to the caller's geo-IP. `countryCode: FI` works (182 results above). — [/home/user/career-ops/providers/thehub.mjs](/home/user/career-ops/providers/thehub.mjs)
- Teamtailor auto-detection is pinned to `*.teamtailor.com`. Branded hosts such as careers.futurice.com need an explicit `provider: teamtailor`. — [/home/user/career-ops/providers/teamtailor.mjs](/home/user/career-ops/providers/teamtailor.mjs)
- scan.mjs's location vocabulary includes `finland` and `helsinki`. — [/home/user/career-ops/scan.mjs](/home/user/career-ops/scan.mjs) (~line 2276)

### Inferences
- About 25 hand-verified entries would cover the English-language postings of the main Finnish product companies and consultancies with zero-auth APIs. The entries would use the slugs above plus `provider:`/`api:` overrides for Futurice, Fortum, Vaisala, Wärtsilä and Nokia, plus The Hub with `countryCode: FI`. career-ops' provider set is not the bottleneck; the missing Finnish company list is.
- Teamtailor's popularity among Finnish consultancies means many smaller Finnish employers are probably reachable via `<slug>.teamtailor.com/jobs.rss`. This is inferred from 7 of the roughly 50 slugs tested.
- Finnish-native ATSs (Laura, HR-manager/Talentadore) and Nordic ones (Jobylon, Varbi, ReachMee) are likely used by public-sector and traditional Finnish employers. Their postings usually also appear on Duunitori and Työmarkkinatori. A tool that cannot read those two boards will under-cover that segment. This prevalence was not measured.

### Gaps
- ATS for Elisa, OP, Telia Finland and Rovio not determined. Nordea's SuccessFactors status not confirmed. Aiven's Greenhouse slug and Varjo's Workable slug not confirmed.
- No measurement of how widely Laura, HR-manager/Talentadore, Jobylon or Sympa are used among Finnish IT employers.
- The Workday and Oracle boards' Finland posting counts were not queried (the Workday hosts returned 406 to plain curl).

## Q3. Application conventions, salaries, timelines and language

### Takeaway
- **CV and letter:** CVs are 1–2 pages, reverse-chronological and tailored. A photo is optional and common, but check the ad. The application letter (hakemus) runs a little under a page, in the language of the ad. LinkedIn is expected.
- **Salary expectation:** a "palkkatoive" is often asked for. Applicants should state a realistic monthly gross figure and justify it.
- **Pay levels:** the latest Finnish developer salary survey (Koodiklinikka "2025", collected Feb–Mar 2026) gives a median of €5,800/month gross. Medians are about €6,000 in the Helsinki region and about €5,300 in Tampere and Turku. Levels.fyi places Greater Helsinki total compensation at roughly €73–85K. TEK's starter recommendation was €4,260–4,610/month (Dec 2025–May 2026).
- **Process:** consultancy processes are typically 2–3 conversational rounds, often without LeetCode.
- **Language and market:** English-only work is common in software, and English-working respondents report higher pay. But the labour market is weak: trend unemployment was 10.1% in August 2026, and Duunitori ad volume fell 24% in 2025.

### Cited Findings

**CV and application** — all from [InfoFinland – Job application and CV](https://infofinland.fi/work-and-enterprise/find-a-job-in-finland/job-application-and-cv) unless noted
- CV format: "A CV is usually 1–2 pages long"; customise it for each job; reverse-chronological order; a short profile summary at the top; add your LinkedIn profile.
- Photo: allowed, but check the ad, because recruitment can be anonymous.
- Language: "Usually, job applications are written in the language in which the job advertisement was published."
- Application letter: "a little under a page long", answering the ad's requirements. Send attachments as PDFs.
- Salary request: it must be realistic, "not too high but not too low". Unions provide pay data, and pay cannot go below the applicable collective agreement.
- References: they may only be contacted with your consent.
- Video applications: about 1–3 minutes, sent as a link.
- Photo practice varies by source. Some Finnish guides call a photo customary, while others note an anonymous-CV debate. — [Familiary – anatomy of a CV](https://www.familiary.fi/anatomy-of-a-cv.html); [University of Turku rekry](https://sites.utu.fi/rekry/?p=7643) (search summary)
- The City of Espoo advises tailoring the cover letter to the ad's specific requirements. — [Espoo – Navigating the Finnish job market](https://www.espoo.fi/en/articles/navigating-finnish-job-market-insider-tips-industry-professionals) (search summary)

**Palkkatoive (salary expectation)**
- Duunitori advises researching pay levels first, using its comparison of 600+ job titles and union tables. — [Duunitori – palkkatoive](https://duunitori.fi/tyoelama/palkkatoive/) (search summary)
- TEK's salary researcher recommends justifying the figure by the job's demands, your skills and your performance. — [Verkkouutiset](https://www.verkkouutiset.fi/a/palkkatutkija-paljastaa-taman-verran-tyohaastattelussa-voi-vaatia-palkkaa/) (search summary)
- Advice to aim high rather than low comes from an Yle article that is more than 11 years old. — [Yle](https://yle.fi/a/3-7454454)

**Salaries — Koodiklinikka survey "2025"**
- Basics: n = 682, of whom 590 are employees and 92 freelancers. Responses were collected 2026-02-09 to 2026-03-03, and the data is CC BY 4.0. — [Koodiklinikka palkkakysely 2025](https://koodiklinikka.github.io/palkkakysely/2025/)
- Employee monthly salary: median €5,800, mean €6,185. Annual income: median €73,090, mean €89,232. — same page
- My own computation from the survey's [data.csv](https://koodiklinikka.github.io/palkkakysely/2025/data.csv), employees only, monthly base salary:

| Breakdown | Group | n | Median | p25–p75 |
|---|---|---|---|---|
| All employees | — | 588 | €5,800 | €4,900–6,900 |
| City | Helsinki region (PK-seutu) | 348 | €6,000 | €5,150–7,089 |
| City | Tampere | 110 | €5,300 | — |
| City | Turku | 50 | €5,314 | — |
| City | Oulu | 18 | €6,075 | — (small n) |
| City | Jyväskylä | 13 | €5,040 | — (small n) |
| Experience | 3–5 years | 71 | €4,300 | — |
| Experience | 6–10 years | 203 | €5,300 | — |
| Experience | 11–15 years | 129 | €6,424 | — |
| Experience | 16+ years | 173 | €6,700 | — |
| Experience | 0–2 years | 10 | €2,580 | — (n too small; may include part-time) |
| Seniority | Mid-level | 117 | €4,500 | — |
| Seniority | Senior | 298 | €5,800 | — |
| Seniority | Staff/Principal/Lead | 115 | €6,840 | — |
| Working language | English | 162 | €6,561 | — |
| Working language | Both | 243 | €5,700 | — |
| Working language | Finnish | 176 | €5,459 | — |

- Other results from the same data: median year-on-year income change +3%. 574 of 588 respondents report Finnish-language skills, so non-Finnish-speaking foreigners are heavily under-represented.

**Salaries — other sources**
- Levels.fyi, Greater Helsinki software engineers: median total compensation about €73.6K (page updated 2026-04-02); senior median about €84.8K (p25 €71.9K, p75 €111K; updated 2026-07-21). — [Levels.fyi Greater Helsinki](https://www.levels.fyi/t/software-engineer/locations/greater-helsinki); [senior](https://www.levels.fyi/t/software-engineer/levels/senior/locations/greater-helsinki) (search summary; page could not be fetched directly — unverified)
- TEK starter-salary recommendations:
  - €4,260–4,610/month, valid 1 Dec 2025–31 May 2026, for new graduates in expert roles. It may be higher in the Helsinki region. — [TEK](https://www.tek.fi/en/news-blogs/teks-starter-salary-recommendation-is-eur-4260-4610-per-month)
  - The previous range was €4,130–4,540 (Jun–Nov 2025). — [TEK salary recommendations](https://www.tek.fi/salary-recommendations) (search summary)
  - No recommendation for June 2026 onward was found.
- Duunitori: average private-sector software developer salary €4,445/month, based on 2024 data. — [Duunitori palkat – ohjelmistokehittäjä](https://duunitori.fi/palkat/ohjelmistokehittaja) (search summary)

**Hiring process**
- Reaktor: the summer-developer interview is "a 60-minute remote conversation with two consultants", "not a memory test", and does not expect code. — [Reaktor – Summer developer interview process](https://www.reaktor.com/trainees-2026/summer-developer-interview-process) (search summary)
- One 2025 Glassdoor review of Reaktor describes 3 rounds (intro, attitude, technical), no LeetCode, and about 2 weeks from first interview to offer. This is a single anecdote. — [Glassdoor (fr.ch)](https://fr.glassdoor.ch/Entretien/Reaktor-Entretien-E589428-RVW97280611.htm) (search summary)
- Futurice: two phases (an initial call, then formal meetings), typically two meetings, one of them about culture and people. — [Futurice blog – interview process](https://futurice.com/blog/futurices-interview-process) (search summary)

**Language**
- A December 2025 Reddit post (mirror) claims about 90% of engineering students who get jobs in Finland have zero Finnish. The thread was divided (51% upvoted). — [Reddit mirror](https://reddit.sentinel-team.org/posts/1po1jdh/snapshots/2025-12-16T19%3A01%3A00.06561Z) (anecdotal)
- Older forum reports describe rejections for lacking Finnish. — [Finland Forum](https://www.finlandforum.org/viewtopic.php?p=585107)

**Market conditions**
- Statistics Finland trend unemployment (ages 15–74): 10.3% in January 2026, 10.8% in May, 10.1% in August. The unadjusted May rate of 12.7% was the highest this century. — [Statistics Finland LFS Aug 2026](https://stat.fi/en/publication/cmfp96le0a4mm07vyv0oyqv4n); [The Star / May peak](https://www.thestar.com.my/news/world/2026/06/25/finland039s-unemployment-rate-climbs-to-highest-level-this-century-in-may) (search summary)
- Duunitori ad volume was down about 24% in 2025 vs 2024, per Duunitori's own figures cited in Q1. — [Duunitori 2025](https://duunitori.fi/tyoelama/luetuimmat-tyopaikkailmoitukset-2025)
- TEK (2022 data): 23% of tech professionals' unemployment spells lasted over 6 months, versus 25% for non-Finnish professionals. — [TEK – unemployment periods](https://www.tek.fi/en/services-and-benefits/research/tek-studies-international-experts/unemployment-periods-of-tech-professionals-in-finland)

### Inferences
- Salary questions in Finland are framed as **monthly gross**. A tool's salary fields and negotiation scripts should accept €/month and convert carefully. The survey collects holiday bonus (lomaraha) separately, so annual figures are not simply 12 × monthly. I did not verify the typical lomaraha size.
- English-only developer roles exist in meaningful numbers: 162 of 588 respondents work only in English, at a higher median. These roles cluster at international product companies (Wolt, Supercell, ICEYE, Smartly, Oura), which are exactly the ATS-API employers. Finnish-language ads dominate the domestic boards. This suggests a language filter (posting language and "Finnish required") is useful.
- Interviews at Finnish consultancies lean toward conversational and value-fit rounds rather than LeetCode. Interview-prep tooling should weight behavioural and consulting-case preparation for this segment.

### Gaps
- No authoritative 2026 count of interview rounds or time-to-offer for Finland. The evidence is company blogs and single anecdotes.
- Levels.fyi figures could not be fetched directly.
- No current statistic on the share of IT postings that require Finnish.
- The TEK salary survey for software roles specifically was not found.

## Q4. Work permits and relocation for non-EU candidates

### Takeaway
A non-EU software engineer normally comes on a **specialist residence permit** or an **EU Blue Card**. In 2026 both require at least €3,937/month gross. Both qualify for Migri's **fast track**, which targets a decision in 2 weeks for first permits applied for from abroad. Most mid and senior Finnish developer salaries clear the threshold easily. In Finland, "sponsorship" means an employer willing to hire from abroad and complete the employer part in Enter Finland, not US-style sponsorship.

### Cited Findings
- **Specialist permit** — [Migri – Specialist](https://migri.fi/en/specialist)
  - Who qualifies: expert duties requiring special expertise; the page explicitly lists "IT experts".
  - Salary: at least **€3,937/month in 2026**; fringe benefits do not count.
  - Education: a higher-education degree, or equivalent expertise from work.
  - Confirmed employment is required before applying.
  - The first permit lasts up to 2 years.
  - Fees: €530 electronic, €630 paper.
  - "You can apply … via the fast-track service and get the permit in two weeks."
- **EU Blue Card** — [Migri – EU Blue Card](https://migri.fi/en/eu-blue-card)
  - Salary: at least **€3,937/month in 2026**.
  - The work must last at least six months.
  - Education: a degree of at least 3 years, or usually at least 5 years of comparable professional experience.
  - Fees are the same as the specialist permit, and fast track is available.
- **Fast track** — [Migri – Fast track](https://migri.fi/en/fast-track)
  - First permits only, and only if not already in Finland.
  - Apply in Enter Finland and prove identity within 5 working days.
  - The employer adds the terms of employment via Enter Finland for Employers within 2 working days.
  - A D visa can be requested at the same time, allowing arrival right after the decision.
- **Talent Boost**: Work in Finland states it "is part of Talent Boost program". — [Work in Finland](https://www.workinfinland.com/en/); [TEM – Talent Boost](https://tem.fi/en/talent-boost-en)
- **career-ops visa filter**
  - Its default vocabulary covers US, Singapore, EU Blue Card and UK wording.
  - Relocation wording is "deliberately excluded: relocation != sponsorship".
  - It reads job description text, so it only works with providers that return descriptions.
  - Sources: [/home/user/career-ops/scan.mjs](/home/user/career-ops/scan.mjs) (~lines 1005–1045); [/home/user/career-ops/templates/portals.example.yml](/home/user/career-ops/templates/portals.example.yml) (~lines 380–420)

### Inferences
- The €3,937 threshold sits below the Koodiklinikka 3–5-year median (€4,300) and the TEK starter range (€4,260+). So it constrains mainly junior roles. The specialist permit also allows "equivalent expertise" without a degree, which may matter for self-taught developers.
- A "visa sponsorship" filter has limited value in Finland. Postings by Finnish employers rarely use US-style "sponsor" wording; that is inferred and not measured. A more useful signal would be phrases like "relocation support/package", "we support with work permits", or "residence permit". career-ops would need custom `positive` keywords for this, and they would only fire on description-bearing providers.

### Gaps
- Current Migri processing-time statistics and the rate at which fast-track applications meet the 2-week target were not retrieved.
- No data on how many Finnish tech employers actually hire from outside the EU.

## Q5. Which job tools realistically cover Finnish postings, and what a Finland-targeting user must fill in

### Takeaway
- **career-ops:** can cover the high-value English-language segment well, but only after the user adds Finnish employers. Its providers already read the ATSs found in Q2; the shipped template has no Finnish companies, and The Hub must be set to `countryCode: FI`.
- **JobSpy:** covers LinkedIn (global search by location) and Indeed Finland.
- **No tool here legitimately ingests** Duunitori or Työmarkkinatori. The workarounds are their e-mail alerts, manual pasting, or a formal Työmarkkinatori API agreement.
- Agencies and the hidden job market need networking workflows, not scanners.

### Cited Findings
- **JobSpy**
  - Supported sites: LinkedIn, Indeed, Glassdoor, ZipRecruiter, Bayt, Naukri, BDJobs and HelloWork.
  - Finland is a supported Indeed country (`country_indeed="Finland"`); Glassdoor does not support Finland.
  - "LinkedIn searches globally & uses only the `location` parameter", and LinkedIn rate-limits bursts with HTTP 429.
  - Source: [JobSpy README](https://github.com/speedyapply/JobSpy)
- **career-ops capabilities**: it has providers for every ATS confirmed in Q2 (greenhouse, ashby, teamtailor, workday, successfactors, oraclecloud, smartrecruiters, workable) plus thehub, and none for Duunitori, Työmarkkinatori, Jobly, LinkedIn or Indeed. — [/home/user/career-ops/providers/](/home/user/career-ops/providers/)
- **career-ops LinkedIn and aggregator policy**
  - LinkedIn and other aggregator listings are treated as UNCONFIRMED until the role is found on the employer's own careers page or ATS.
  - LinkedIn JD loading allows one browser attempt per posting, with no scraping workarounds.
  - Source: [/home/user/career-ops/AGENTS.md](/home/user/career-ops/AGENTS.md) ("Aggregator Listings" and "LinkedIn JD loading guard")
- **career-ops Finland-specific gaps**
  - Market modes exist for da, de, nl, pl and others, but there is no `modes/fi`. — [/home/user/career-ops/modes/](/home/user/career-ops/modes/)
  - The `modes/regional/eu-swe.md` calibration mode never mentions Finland. — [/home/user/career-ops/modes/regional/eu-swe.md](/home/user/career-ops/modes/regional/eu-swe.md)
- **career-ops location filter**: onboarding guidance says that for non-US countries the main cities should be added as well as the country, because a posting may name only the city. For Finland that means Helsinki, Espoo, Vantaa, Tampere, Turku, Oulu and Jyväskylä. — [/home/user/career-ops/AGENTS.md](/home/user/career-ops/AGENTS.md) (Onboarding Step 3)
- **Finnish boards have no compliant automated route**
  - Duunitori's terms forbid scraping, and its robots.txt disallows all user agents.
  - Työmarkkinatori's API is credentialed.
  - Third-party Apify scrapers exist for both but are unofficial.
  - Sources: [Duunitori terms](https://duunitori.fi/compliance/kayttoehdot); [KIPA doc](https://tyomarkkinatori.fi/jobpostingprovider/documentation/KIPA-search-jobpostings-fi.html); [Apify](https://apify.com/unfenced-group/duunitori-fi-scraper)

### Inferences
**Practical gap list for a Finland-targeting career-ops user**
1. Add verified `tracked_companies` entries for the Finnish employers in Q2, with the slugs listed there. Use explicit `provider:`/`api:` overrides for Futurice (Teamtailor, branded host), Fortum, Vaisala and Wärtsilä (SuccessFactors), and Nokia (Oracle CX_1).
2. Enable The Hub with `countryCode: FI`.
3. Set `location_filter` to Finland plus its main cities.
4. Track Duunitori and Työmarkkinatori through their own e-mail alerts sent to Gmail, or by pasting JDs.
5. Treat LinkedIn and Indeed hits as leads to confirm at the employer's ATS.
6. Keep a networking/referral track, given TEK's 20–30% public-jobs figure.

**Cloud-assistant angle** (Claude with GitHub, Gmail and Drive connectors)
- Gmail is the natural ingestion point for Duunivahti, Työmarkkinatori, LinkedIn and agency alerts, and for recruiter replies.
- Drive, Docs and Sheets fit the tracker and tailored-CV storage.
- The zero-auth ATS APIs (Greenhouse, Ashby, Teamtailor RSS, SmartRecruiters, The Hub) are reachable from a cloud container: all responded in this session's probes.
- Workday, LinkedIn, Indeed and some corporate career sites showed bot-blocking to plain HTTP (406, 401, 403 or connection resets) and may need browser-based fetching.
- A Finland-aware tool should also handle:
  - monthly-gross salary framing and the palkkatoive field;
  - Finnish-language JDs ("hakemus", "palkkatoive", "suomen kielen taito" / Finnish-language skill);
  - a "Finnish required" flag;
  - permit-friendly signals (relocation and residence-permit wording) rather than US "sponsorship" keywords.

### Gaps
- How much of the Finnish software market appears only on Duunitori or Työmarkkinatori, and not on employer ATS boards or LinkedIn, was not measured.
- LinkedIn's Finland job counts and the practical success rate of JobSpy's Finland Indeed scraping were not tested in this session (fi.indeed.com returned 401 to plain curl).
- I could not determine whether any open-source tool other than career-ops (and JobSpy for LinkedIn/Indeed) has Finnish board support. A GitHub search for Duunitori or Työmarkkinatori scrapers was not performed.
