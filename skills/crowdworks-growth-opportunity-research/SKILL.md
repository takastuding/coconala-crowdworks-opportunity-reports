---
name: crowdworks-growth-opportunity-research
description: Research and rank public CrowdWorks or similar Japanese freelance opportunities for side work using Japanese labor/social-insurance knowledge, 社労士 positioning, FP1級 or financial-planning skills, beginner-friendly article writing, weekend-focused availability, portfolio building, client-safety screening, Japanese proposal drafting, and Markdown reports saved to GitHub. Use when Codex is asked to find, compare, report, save, or draft applications for CrowdWorks案件 around 社労士, 労務, 社会保険, 年金, FP, 保険, 家計, 資産形成, ライフプラン, 記事執筆, ライター, コラム, 監修, or similar opportunities.
---

# CrowdWorks Growth Opportunity Research

## Purpose

Find public freelance opportunities that fit the user's current stage:

- 社労士-related expertise and FP1級 skill.
- Limited weekday capacity; weekend-focused work is preferred.
- Article-writing experience is still being built.
- Early low fees are acceptable for portfolio value, but exploitative conditions are not.
- The strategic goal is credible writing, checking, supervision, or light expert-support experience around labor, social insurance, money, benefits, household finance, insurance, pensions, and life planning.

Optimize for growth and reputation, not only immediate pay. Treat client safety as part of the ranking, not an optional appendix.

## Required Source Boundary

Use only public information. Do not apply, send, post, publish, delete, contact clients, contact CrowdWorks users, or use private/personal data. Stop at research, drafts, notes, commits, and approval points.

## Research Workflow

1. Read repository or automation memory if provided so recent searches are not repeated blindly.
2. Confirm current listings by searching CrowdWorks/public web directly. Do not rely on memory for active案件.
3. Search broadly, then narrow. Prefer several targeted searches over one broad query.
4. Extract concrete listing facts: title, URL, status/deadline, reward, word count or volume, expected cadence, required experience, communication tools, source/tax/copyright notes, client review count, identity verification, and 発注ルールチェック.
5. Evaluate candidates with `references/evaluation-guide.md` before writing the final report.
6. Downgrade attractive案件 to B/C/D when safety or workload risk is material.
8. Before writing the report, check the previous expected run date. If there is no matching report file, same-day memory entry, or same-day session trace, treat it as a missed run and mention it in memory and in the next report.
9. Save the report when the automation asks for repository output. For this user's recurring CrowdWorks report flow, default to GitHub repository `takastuding/coconala-crowdworks-opportunity-reports` and path `reports/YYYY-MM-DD-crowdworks-report.md` unless the user explicitly names a different repository or path. Do not assume the current working repository is the save target.
10. Use the fixed GitHub save sequence: check path, create or update only the current platform file, verify `html_url`, then record the commit URL.
11. Before finishing an automation run, append a UTF-8 memory entry with `Fetch method`, `Saved report`, `Commit`, `Failure`, and `Next expected run`, as well as the top A/B/C/D candidates and excluded repeat candidates.

## CrowdWorks Fetching Notes

CrowdWorks public search pages often embed listings in the `vue-container` element as HTML-escaped JSON. If browser search is sparse or `Invoke-WebRequest` fails:

1. Prefer direct public URLs such as:
   `https://crowdworks.jp/public/jobs/search?search%5Bkeywords%5D=<urlencoded keyword>`
2. If PowerShell `Invoke-WebRequest` disconnects, try `curl.exe`.
3. In this environment, proxy variables may point to `127.0.0.1:9`; use `curl.exe --noproxy "*" -s -L --compressed -o <tmpfile> <url>` when needed.
4. Parse `<div id="vue-container" data="...">`; HTML-decode the `data` attribute and read `searchResult.job_offers`.
5. Fetch detail pages for top candidates and inspect the public text for: 本人確認, 発注ルールチェック, レビュー件数, 報酬, 納期, 源泉徴収, 著作権, 外部連絡, 実名/顔写真/資格名掲載, 修正回数, and responsibility boundaries.
6. If fetching is partial, state the limitation and rank conservatively. Do not invent listings.

## GitHub Report Saving Notes

When the report must be saved to `takastuding/coconala-crowdworks-opportunity-reports` or another GitHub repository:

1. Prefer an existing local checkout of the target repository if available. If the local checkout is unavailable, use `gh api` against the target repository instead of saving into an unrelated current repository.
2. Save CrowdWorks reports as `reports/YYYY-MM-DD-crowdworks-report.md` unless the user requests another filename.
3. For simple create/update through GitHub, check the path with `gh api repos/<owner>/<repo>/contents/<path>`, then use the GitHub Contents API with base64 content and `sha` when updating.
4. If Contents API is awkward for a larger Markdown file, create a blob from a temp file, create a tree and commit, then update `refs/heads/<branch>`.
5. Verify the saved file with `gh api repos/<owner>/<repo>/contents/<path> --jq '{html_url:.html_url, sha:.sha, size:.size}'` or by checking the local commit and push result.
6. Include the saved file URL or commit hash in the final response.
7. On a same-day rerun, update only `reports/YYYY-MM-DD-crowdworks-report.md` with its current `sha`; never modify a Coconala report.

## Search Priorities

Prioritize in this order:

1. Beginner-friendly expert writing: articles, columns, SEO drafts, explainer content, supervised drafts, newsletter/blog work.
2. Credential-differentiated writing or supervision: 社労士/FP knowledge is useful even if writing experience is not mandatory.
3. Light expert support: fact-checking, outline creation, Q&A drafts, learning material drafts, benefits/pension/insurance explainers.
4. Weekend-compatible adjacent work: research, document summaries, small content batches, one-off consultation support.

Useful keywords:

- 社労士 記事執筆
- 社会保険労務士 ライター
- 労務 記事
- 労務 チェック
- 社会保険 記事
- 年金 記事
- 年金 台本
- 社会保障 ライター
- FP 記事執筆
- FP1級 監修
- CFP 監修
- ファイナンシャルプランナー ライター
- 保険 記事執筆
- 家計 記事
- 資産形成 ライター
- ライフプラン 記事
- 監修 FP
- 監修 社労士

## Caution Rules

Downgrade to B or lower when any of these appear:

- Client has no reviews, no identity verification, or unanswered 発注ルールチェック.
- The listing asks to start before escrow, move off platform before contract, or use external tools before contract.
- The listing asks the worker to uncheck source withholding without a clear reason.
- Real name, face photo, profile, qualification, or supervisor credit will be published.
- The task asks for product endorsement, investment/tax/labor/legal advice, or claims that may overstate eligibility or benefits.
- Scope is vague, deadline is inconsistent, revision count is unclear, or workload is too high for weekend work.
- Pay is extremely low relative to word count, test work is repeated/unpaid, or monthly volume is large.
- Experience requirements conflict with the user's current stage.

Downgrade to D when reputation, legal/tax, or professional-responsibility risk is high and cannot be reduced with pre-application questions.

## Output Format

Write in Japanese. Keep it smartphone-readable.

Include:

1. `調査日時`
2. `今日の結論`: up to three best actions or案件. Be honest when there is no A-tier candidate.
3. `優先候補`: table with `総合`, `案件名`, `URL`, `分類`, `案件テーマ`, `成長価値`, `土日対応`, `発注者安全性`, `懸念点`, `応募メモ`.
4. `応募前に確認すること`: concrete questions for every A/B candidate.
5. `除外した案件・理由`: short reasons for unsuitable, risky, expired, or too-demanding案件.
6. `検索したキーワード`
7. `次回の見直し条件`
8. `応募文たたき台`: one tailored Japanese proposal for the top candidate.

When no strong案件 are found, still report searched keywords, weak candidates, and what should change next time.

## Application Draft Rules

Write proposals that are honest and confident:

- State that writing experience is being built without sounding apologetic.
- Lead with 社労士/FP1級 knowledge, careful research, and plain-language explanation.
- Make weekend availability explicit: `本業があるため平日日中の即時対応は難しい場合がありますが、土日を中心にまとまった作業時間を確保できます。`
- Offer a low-friction first step: one article, one outline, one check pass, or a small trial.
- Avoid promising legal, tax, investment, or labor advice. Frame output as article writing, research, explanation, draft creation, fact-checking, or supervised content support unless the listing clearly defines expert supervision.

## Verification

For Markdown report edits:

1. Run `git diff --check` when possible.
2. If unrelated pre-existing files make full `git diff --check` fail, run `git diff --check -- <changed report>` and report the unrelated blocker separately.
3. Review the report for accidental personal data and wording that implies applying, sending, posting, contacting, or contracting.
4. Stage/commit only the intended report file in the target repository unless the user explicitly asks for broader cleanup.

## Resources

Read `references/evaluation-guide.md` when ranking案件 or writing the final report.


## Automation Logging

For recurring automation runs, keep memory entries concise and UTF-8:

- Run started: <ISO8601 timestamp>
- Target report date: YYYY-MM-DD
- Previous successful report date: YYYY-MM-DD or none
- Fetch method: direct-html | alternate-url | web-search
- Saved report: <file URL>
- Commit: <commit URL>
- Failure: none | github-save:<stage> | fetch:<stage> | missed-run-detected:<date>
- Next expected run: <ISO8601 timestamp>
