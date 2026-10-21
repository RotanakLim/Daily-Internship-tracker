Update data/postings.json. The user is a second-year Computer Science student at Cal Poly San Luis Obispo, graduating May 2029. This runs unattended, so don't ask questions. Use web search and open each posting page to verify everything.

NEW postings must meet ALL of these:

1. Track: swe (SWE/backend/frontend/full-stack/mobile/ML eng), pm (APM/product intern), it (help desk, sysadmin, network, IT ops), sec (security eng, SOC, cyber ops, pen testing, cloud security; not pure IT/financial audit), devops (DevOps, SRE, platform, cloud/infra, build/release, CI/CD).
2. Term is Summer 2027.
3. Location is in the US (in person, hybrid or remote).
4. Explicitly accepts 2029 grads (class of 2029, sophomores, graduating Dec 2027 or later) or states no grad-year requirement. Exclude postings limited to 2027/2028 grads, juniors/rising seniors only, or grad students only.
5. Currently open.
6. The posting page itself names Computer Science as an accepted major.

Steps:

1. Load data/postings.json. Never change an existing posting's status or any field except checkedAt, closed, closedAt, closedReason, and postedDate/postedApprox (only when postedDate is missing).
2. Re-check up to 30 postings that aren't closed, oldest checkedAt first. Mark one closed only on clear evidence: says no longer accepting/expired/filled, 404, redirects to a generic search, or a firm deadline has passed. A failed or blocked fetch is never evidence. Set checkedAt on each.
3. Search each track separately: company career pages, the SimplifyJobs Summer2027-Internships GitHub list, LinkedIn/Indeed, sophomore programs (Microsoft Explore, Google, Meta, Capital One), public-sector/university IT, and federal, Federal Reserve, defense and cloud/infra cyber and DevOps programs.
4. Add up to ~30 new postings not already present (match by URL or by company + title, including closed ones). Include at least 3–4 each for PM, IT, Cybersecurity and DevOps when verified ones exist. Never pad the list with unverified or ineligible postings.
5. postedDate: use only a labeled date on the posting page ('Posted Date', 'Date posted', 'Posted on', JSON-LD datePosted). If the page only says 'N days ago', compute the date and set postedApprox: true. Otherwise null. Never use deadlines, start dates or page-modified dates. Ignore a date later than firstSeen.
6. id = lowercase slug of '<company>-<title>' (a-z, 0-9, hyphens, max 120 chars). Set status 'new', firstSeen = today (Pacific), and firstSeenAt = checkedAt = now (UTC).
7. Append {at, newCount, closedCount, checkedCount} to data/runs.json. Validate both files as JSON, then commit 'Daily internship search <date>' and push.
8. Write summary.md: 'Internship search — <weekday, month day, h:mm AM/PM PT>: N new postings', one line per posting (**Company — Role** · location · grad rule · posted date if known · [Apply](url)) grouped by track (omit empty groups), then a 'Closed since last search' section. Print it as well.
