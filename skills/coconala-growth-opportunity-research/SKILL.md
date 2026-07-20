---
name: coconala-growth-opportunity-research
description: Use when Codex needs to research Coconala opportunities for the user, including Coconala job matching, buyer requests, public service/category market signals, competitor/service analysis, buyer-demand scouting, weekend-safe side-business opportunities using shakaihoken/labor knowledge, sharoushi credentials, FP1, pensions, insurance, household finance, retirement, benefits, writing, and drafting Japanese proposals or Coconala service revisions.
---

# Coconala Growth Opportunity Research

## Overview

Help the user find Coconala opportunities that fit their current stage: limited weekday capacity, weekend-focused availability, still building public writing/client-work proof, and wanting to turn sharoushi and FP1 knowledge into small, credible side-business results.

Coconala is not only an application marketplace. Always separate these two tracks:

- **Jobs and requests**: buyer-posted single/spot jobs and ongoing hourly/monthly jobs. Evaluate these like CrowdWorks listings.
- **Market signals**: existing services, category pages, rankings, blogs, and know-how listings. Use these to recommend the user's own service, profile, blog, title, price, or offer improvements. Do not treat competitor services as jobs to apply to.

Treat **retirement consultation and retirement-adjacent concerns** as a primary target area, not a side keyword. Look for people who need help organizing questions around resignation, unemployment insurance, health insurance, pension enrollment, injury/sickness allowance, final salary/paid leave, career transition, household cash flow after leaving work, and what to ask public offices or professionals next. Prefer safe text-based consulting, explanation, checklist, and pre-consultation organization work over application filing or outcome guarantees.

Optimize for growth, reputation safety, and realistic weekend execution, not only immediate revenue.

## Workflow

1. Read automation or repository memory when provided. Use it to avoid repeating recent weak candidates, but never rely on memory for active listings.
2. At the start of an automation run, append a UTF-8 memory entry with these labels:
   - `Run started`
   - `Target report date`
   - `Previous successful report date`
   - `Next expected run`
3. Confirm the latest Coconala pages by searching the web or the platform directly.
4. Search buyer-posted opportunities first:
   - Coconala work index: `https://coconala.com/job_matching/supplier`
   - Spot/request categories such as writing (`/requests/categories/19`) and consulting/professionals (`/requests/categories/27`)
   - Ongoing job categories such as financial professionals (`/job_matching/outsources/jobs/24`) and licensed/professional work (`/job_matching/outsources/jobs/25`)
5. Search market signals next:
   - Writing services (`https://coconala.com/categories/19`)
   - Consulting/professional services (`https://coconala.com/categories/27`)
   - Asset management/side-business consultation (`https://coconala.com/categories/17`)
   - Retirement, career, labor, and life-event consultation services, including Coconala category/search pages for `退職相談`, `退職代行ではない相談`, `傷病手当金`, `失業保険`, `社会保険`, `年金`, `転職相談`, and `キャリア相談`.
   - Coconala blogs and know-how pages when they reveal buyer concerns or proven titles.
6. Use narrow searches with Coconala plus terms such as `社労士`, `社会保険労務士`, `労務`, `退職`, `退職相談`, `退職前`, `退職後`, `退職したい`, `会社を辞めたい`, `有給消化`, `離職票`, `傷病手当金`, `失業保険`, `雇用保険`, `健康保険`, `国民健康保険`, `任意継続`, `社会保険`, `年金`, `就業規則`, `転職相談`, `キャリア相談`, `FP1級`, `FP`, `ファイナンシャルプランナー`, `保険`, `家計`, `資産形成`, `ライフプラン`, `記事執筆`, `ライター`, `監修`, `コラム`, `相談`.
7. Fix the fetch fallback order and record the method actually used:
   - direct HTML fetch
   - alternate public URLs or category pages
   - web search and public snippets
8. Rank jobs and market signals with `references/evaluation-guide.md`.
9. Downgrade anything with unclear scope, weekday-heavy operations, professional-liability ambiguity, credential/reputation risk, or off-platform pressure.
10. Before writing the report, check the previous expected run date. If there is no matching report file, same-day memory entry, or same-day session trace, treat it as a missed run and mention it in memory and in the next report.
11. Save the report when the user asks for the recurring report flow. Prefer `reports/YYYY-MM-DD-coconala-report.md` in GitHub repository `takastuding/coconala-crowdworks-opportunity-reports` unless the user explicitly names another repository. If the local repo/remote is unavailable, use `gh api` GitHub Contents API or Git Data API to create/update the same path.
12. Use a fixed GitHub save sequence:
   - check path
   - create or update file
   - verify `html_url`
   - record commit URL
13. Before finishing an automation run, append a UTF-8 memory entry with:
   - `Fetch method`
   - `Saved report`
   - `Commit`
   - `Failure`
   - `Next expected run`

## Coconala Fetching Notes

Coconala public pages can be large and partly client-rendered, but search and request pages often include enough server-rendered HTML to extract useful facts.

- Prefer direct public URLs:
  - `https://coconala.com/requests?keyword=<urlencoded keyword>`
  - `https://coconala.com/search?keyword=<urlencoded keyword>`
  - `https://coconala.com/requests/<id>`
  - `https://coconala.com/services/<id>`
- If web search snippets are sparse, fetch pages directly with `curl.exe -L --max-time 60 -s -o <tmpfile> <url>`.
- Read cached HTML as UTF-8. On Windows, PowerShell's default decoding can display mojibake; use `Get-Content -Encoding UTF8`.
- For request pages, look for `/requests/<id>` cards and extract `c-itemInfo_category`, `c-itemInfo_title`, `c-itemInfo_description`, `投稿日時`, `d-requestBudget`, `応募者数`, and `募集期限`.
- For service search pages, look for `/services/<id>` blocks and extract `c-serviceListItemColContentHeader_overview`, `catchphrase`, `description`, seller name, price, rating, and review count.
- Treat repeated request IDs across keyword searches as one candidate. Record which keywords surfaced it, but rank once.
- Direct detail pages may have different markup from search cards; use meta title/description and nearby text as fallback.
- If fetching is partial, state the limitation and rank conservatively. Do not invent listings.

## GitHub Report Saving Notes

For the recurring report flow, use `takastuding/coconala-crowdworks-opportunity-reports`. When the report must be saved to another GitHub repository:

1. Check whether the path exists with `gh api repos/<owner>/<repo>/contents/<path>`.
2. For simple create/update, use GitHub Contents API with base64 content and `sha` when updating.
3. If shell pipes or local writes are blocked, create a Git blob from an existing temp file with `gh api -X POST repos/<owner>/<repo>/git/blobs -F content=@<file> -f encoding=utf-8`, then create tree, commit, and update `refs/heads/<branch>`.
4. Verify with `gh api repos/<owner>/<repo>/contents/<path> --jq '{html_url:.html_url, sha:.sha, size:.size}'`.
5. Include the saved file URL or commit URL in the final response.
6. On failure, write `Failure: github-save:<stage>` to memory before exiting.
7. On a same-day rerun, update only `reports/YYYY-MM-DD-coconala-report.md` with its current `sha`; never modify a CrowdWorks report.

## User Fit

Assume this baseline unless the user updates it:

- The user has sharoushi-related expertise and FP1 skill.
- The user is still building article-writing and public Coconala proof.
- The user can accept lower early fees for proof, but should avoid exploitative work.
- The user mainly works on weekends and cannot sustain weekday-heavy chat, phone, or operational support.
- The user's strategic goal is to build credible proof around labor, social insurance, money, benefits, household finance, insurance, pensions, retirement, and life planning.

## Search Priorities

Prioritize in this order:

1. Retirement-consultation fit: text-based requests or market signals around resignation, unemployment insurance, social insurance, pensions, injury/sickness allowance, paid leave, career transition, or household cash flow after leaving work.
2. Beginner-friendly expert writing: articles, columns, SEO drafts, explainers, newsletters, blog posts, and supervised drafts around labor, social insurance, pensions, insurance, household finance, and retirement.
3. Coconala spot jobs where sharoushi/FP knowledge differentiates the user and scope is fixed.
4. Market signals that can improve the user's own retirement/labor/FP services: strong buyer pain, clear service title patterns, low-risk starter offers, price anchors, and blog topics.
5. Light expert support: outlines, fact-checking, Q&A drafts, benefits/pension/insurance explainers, consultation-preparation memos, and content review under clear responsibility boundaries.
6. Weekend-compatible adjacent work: research, document summaries, one-off consultation preparation, small content batches, and asynchronous text consultation.

Be cautious with:

- `申請代行`, `絶対にもらえる`, `確実に節税`, `必ず受給`, `丸投げ`, or other outcome-guarantee wording.
- Daily chat, weekday daytime calls, urgent turnaround, long-running operations, or open-ended support.
- Very low fees with large volume, unpaid tests, unclear ownership, vague scope, or requests to copy existing content.
- Work that requires licensed professional responsibility beyond the user's intended role.
- Requests to use the user's name, qualification, or supervision label in promotional claims without clear final responsibility.
- Off-platform communication, payment before platform contract, or moving to LINE/DM before terms are clear.
- Retirement-related requests that ask the user to act as a退職代行, negotiate with an employer, guarantee benefit eligibility, submit forms, or give individualized legal/labor conclusions without a properly scoped professional engagement.

## Output Format

Use Japanese. Include:

- `調査日時`
- `今日の結論`: up to three best actions. Mix direct applications and service-improvement actions when useful.
- `応募・対応候補`: table with `総合`, `対象名`, `URL`, `種別`, `テーマ`, `成長価値`, `土日対応`, `安全性`, `懸念点`, `次アクション`.
- `退職相談マッチ候補`: when any retirement-adjacent signal exists, summarize whether it is a direct job, service-market signal, blog topic, or existing-service improvement target.
- `市場シグナル・出品改善`: table with `示唆`, `根拠URL`, `買い手ニーズ`, `既存出品への活かし方`, `優先度`.
- `除外した案件・理由`: summarize briefly.
- `応募前・出品前に確認すること`: concrete questions/checks for A/B candidates or service revisions.
- `応募文または見積もり相談返信のたたき台`: one tailored Japanese draft for the top job. If no good job exists, write a Coconala service title/description improvement draft instead.
- `次回の見直し条件`: searched keywords, weak signals, and what should change next time.

When no strong jobs are found, do not invent listings. Report the searches, weak candidates, and the best service/profile/blog improvements instead.

When a missed scheduled run is detected, add a short note near the top of the report that an earlier scheduled run appears to have been missed and that the current report is the latest available snapshot.

## Drafting Rules

Write proposals and service copy that are honest and confident:

- Mention that public writing/client proof is still being built only when relevant, and frame it as a reason for careful, modest-scope work.
- Lead with sharoushi/FP1 knowledge, careful research, plain-language explanation, and asynchronous weekend execution.
- Keep boundaries clear: article writing, explanation, draft creation, research support, or consultation preparation unless the job clearly fits licensed professional work.
- Avoid overpromising legal, tax, investment, benefit eligibility, subsidy, or labor outcomes.
- Prefer a low-friction first step: one article, one outline, one text consultation, a trial review, or a small fixed-scope service.

## Automation Logging

For recurring automation runs, memory updates must be UTF-8 and concise. A good final entry shape is:

- `Run started: <ISO8601 timestamp>`
- `Target report date: YYYY-MM-DD`
- `Fetch method: direct-html | alternate-url | web-search`
- `Saved report: <file URL>`
- `Commit: <commit URL>`
- `Failure: <stage or none>`
- `Next expected run: <ISO8601 timestamp>`

## Resources

Read `references/evaluation-guide.md` when ranking jobs, interpreting service-market signals, or writing the final report.
