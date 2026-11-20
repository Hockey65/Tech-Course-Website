# Search Result Validity Review: Course Recommendation Report

**Retrieval date shown in app:** 2026-11-03
**Retrieval method shown in app:** Tavily live research
**Scope:** Two test runs of the "evidence-based report" feature, reviewed from screenshots.

## Summary

Both runs return results that are mostly invalid for the inputs given. The main failures:

1. **Role mismatch.** A "Software engineer" query returns only cybersecurity content.
2. **Articles ranked as courses.** Top-ranked items are listicles and explainer blog posts, not courses.
3. **Job alignment is unreliable.** It is 10/30 on irrelevant skill signals in Case 1 and 0/30 on every result in Case 2.
4. **Budget and goals are effectively ignored.** "Value" is 0/15 for all five results, and "User fit" is 0/10 for four of five results.
5. **Stale or suspicious source dates.** One page is dated 2012, and two "[2026]" pages carry a Dec 2025 date.
6. **Ranking is inconsistent.** The most role-relevant result in Case 2 ranks last.

The app labels every score "Provisional," which is an admission that the scores are not trustworthy. They are still used to produce a ranked list.

---

## Case 1: Software engineer (Montreal)



### Inputs

| Field | Value |
|---|---|
| Target role | Software engineer |
| Experience | 8 months |
| Location | Montreal |
| Budget | CAD 2,500.00 |
| Goal | "I need more help to better understand the basic concepts." |

### Outputs

The app reports 2 provider pages and 2 job postings. The skill signals it says it observed in job postings were *Penetration testing, Governance and risk, Cryptography*.

| Rank | Result | Score | Job alignment /30 | Practical /25 | Credential /20 | Value /15 | User fit /10 |
|---|---|---|---|---|---|---|---|
| 1 | Coursera: "Best Cybersecurity Courses & Certificates [2026]" | 45 | 10 | 25 | 10 | 0 | 0 |
| 2 | SANS: "Cybersecurity Courses \| SANS Institute" | 35 | 10 | 25 | 0 | 0 | 0 |

### Problems

| # | Issue | Evidence |
|---|---|---|
| 1 | **Wrong field.** The user asked for software engineer. Every observed skill signal (penetration testing, governance and risk, cryptography) and both results are cybersecurity. | Skill signals in the research summary; both result titles |
| 2 | **Job postings don't match the role.** The postings supposedly retrieved for "Software engineer near Montreal" yielded security skills. Either the postings were not for software engineering or skill extraction is wrong. | "Observed job skill signals" line |
| 3 | **Rank 1 is a listicle, not a course.** "Best Cybersecurity Courses & Certificates" is a roundup page. It cannot be enrolled in, priced, or completed. | Result title |
| 4 | **Rank 2 is a vendor catalog landing page.** It is not a specific course, and it is dated 2012. | "Page date: Thu, 30 Aug 2012" |
| 5 | **Stale source.** A 2012 page was used as evidence in a 2026 report. | Same date line |
| 6 | **Budget not used.** The user gave CAD 2,500, yet "Value" is 0/15 for both results. No price was extracted. | Score tiles |
| 7 | **Goal not used.** The user wants *basic concepts* help. "User fit" is 0/10 for both. SANS is professional-level training, not a beginner fundamentals resource. | Score tiles |
| 8 | **"Practical work" score unsupported.** Both generic landing pages receive the maximum 25/25 for practical work, which seems implausible for pages that are not courses. | Score tiles |
| 9 | **Weak match claim.** The report says it "Matched 1 of 3 observed skill signals," so even by its own measure the match is poor, and those signals are for the wrong field. | Card description text |
| 10 | **Thin evidence.** The ranking rests on 2 results and 2 postings. | "Course options: 2, Job postings: 2" |

**Verdict:** Invalid. The recommendations do not correspond to the requested role, skill level, or budget.

---

## Case 2: SOC analyst (Ontario)



### Inputs

| Field | Value |
|---|---|
| Target role | SOC analyst |
| Experience | 1.5 years |
| Location | Ontario |
| Budget | CAD 1,500.00 |
| Goal | "Learn more and better further my career" |

### Outputs

The app reports 6 provider pages and 2 job postings, with 3 course options returned. It states the observed job skill signals were *"no verified posting skill signals."*

| Rank | Result | Score | Job alignment /30 | Practical /25 | Credential /20 | Value /15 | User fit /10 |
|---|---|---|---|---|---|---|---|
| 1 | Coursera: "What Is the SSCP Certification? 2026 Guide" | 45 | 0 | 25 | 10 | 0 | 10 |
| 2 | Coursera: "10 Popular Cybersecurity Certifications [2026 Updated]" | 25 | 0 | 0 | 15 | 0 | 10 |
| 3 | TryHackMe: "SOC Level 1 Training" | 25 | 0 | 25 | 0 | 0 | 0 |

### Problems

| # | Issue | Evidence |
|---|---|---|
| 1 | **No job evidence at all.** Zero verified skill signals were found, so job alignment is 0/30 for all three results. The 30-point component is empty, yet a ranked list is still presented. | Research summary; score tiles |
| 2 | **Rank 1 is an explainer article.** "What Is the SSCP Certification?" is a blog-style guide, not a course. | Result title |
| 3 | **Rank 1 is not SOC-specific.** SSCP is a general security-administration certification, so its fit for a SOC analyst is unverified. | Result title; zero job alignment |
| 4 | **Rank 2 is a listicle.** "10 Popular Cybersecurity Certifications" is a roundup, not a course. | Result title |
| 5 | **The most relevant result ranks last.** TryHackMe "SOC Level 1 Training" matches the target role by name, but it is ranked 3rd and gets User fit 0/10. | Rank 3 card |
| 6 | **Tied scores, different ranks.** Ranks 2 and 3 are both 25/100 with no visible tiebreaker. | Score badges |
| 7 | **Budget not used.** The user gave CAD 1,500 and Value is 0/15 for every result. | Score tiles |
| 8 | **Inconsistent user-fit scoring.** The two articles get 10/10 user fit, but the purpose-built SOC training gets 0/10 for the same user. | Score tiles |
| 9 | **Date inconsistencies.** Two different Coursera pages share an identical timestamp (Fri, 05 Dec 2025 00:00:00 GMT) and are labeled "[2026]". This suggests the timestamp is a crawl or placeholder value, not a true publish date. | Page date lines |
| 10 | **Heavy retrieval, little signal.** 6 provider pages were retrieved, but only 3 results survived and none had verified job evidence. | Research summary |

**Verdict:** Invalid. With no verified job evidence, the report's ranking is not meaningful, and it places the role-specific course below generic articles.

---

## Cross-Case Findings

| Pattern | Case 1 | Case 2 |
|---|---|---|
| Top result is an article/listicle, not a course | Yes | Yes |
| Value score is 0 for every result (budget ignored) | Yes | Yes |
| User fit mostly 0 | Yes (both) | Partly (1 of 3) |
| Job alignment unreliable | Wrong-field signals | Zero signals |
| Page date missing, stale, or suspect | 2012 page; one date missing | Identical Dec 2025 stamps; one date missing |
| Scores labeled "Provisional" but still ranked | Yes | Yes |
| Same top score (45/100) despite very different evidence | Yes | Yes |

Both runs give their top result 45/100 despite different inputs and different evidence. Both top results get a 25/25 "Practical work" score from a generic article or landing page. This points to scoring that is driven by page-type heuristics rather than by evidence about each result.

## Suggested Fixes

1. **Filter by result type.** Exclude blog posts, listicles, and category landing pages. Require a specific course or program page.
2. **Validate role relevance before ranking.** If job-posting skills don't match the target role's domain, discard them and flag the run instead of scoring.
3. **Withhold scores when evidence is missing.** If job alignment cannot be verified, show "insufficient evidence" instead of a numeric rank.
4. **Extract price and duration.** Without them, budget-based scoring is impossible, so don't show a Value score of 0 as though it were a real result.
5. **Use the user's goal.** Beginner or "basic concepts" goals should exclude advanced professional training, and role-specific training should not receive User fit 0.
6. **Enforce freshness.** Reject or heavily penalize pages older than a set threshold (for example 2 years), and treat identical timestamps across pages as unreliable.
7. **Add tiebreakers and confidence indicators.** Replace the generic "Provisional" tag with an explicit confidence level and the reason for it.
8. **Test with realistic software-engineering queries.** Case 1 suggests the retrieval may be defaulting to cybersecurity regardless of role.

## Notes on Method

This review is based only on the two screenshots above. The underlying page content and scoring code were not inspected, so causes listed in the fixes are inferences from the visible output.
