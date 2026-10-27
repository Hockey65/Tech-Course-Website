# TechPath: OWASP Top 10 Security Review

**Website:** https://techpath-evidence.polsia.io/\
**Reviewer:** Owen Power\
**Assessment date:** 27 October 2026\
**Assessment type:** Read-only, non-intrusive review\
**Scope:** Public homepage, intake form, results page, and accessible
application source

## 1. Executive summary

This review used the OWASP Top 10:2025 as a framework to assess the
publicly accessible TechPath Evidence application. The supplied
assessment records a SecurityHeaders.com grade of **A** and reports
several common security headers. It also identifies two configuration
items that need confirmation: Content-Security-Policy (CSP) and
Cross-Origin Resource Sharing (CORS).

The review found client-side Zod validation in the intake form.
Client-side validation improves user experience but does not prove that
the server validates incoming requests. Backend validation, rate
limiting, access-control enforcement, dependency versions, and
server-side logging could not be confirmed from the available evidence.

This was not a penetration test. Several findings are unverified and
should be treated as items to investigate, not confirmed
vulnerabilities.

## 2. Scope and methodology

The assessment report states that it reviewed:

-   Public homepage and intake form.
-   Results page, described by the application as a curated sample.
-   The `/api/intake` endpoint through limited, non-intrusive
    observation.
-   Accessible client-side source code, including form validation.
-   HTTP security headers using SecurityHeaders.com.

The assessment avoided destructive testing, credential access,
production configuration changes, and access to other users' data.

### Limitations

-   Backend source code and server configuration were not available for
    full review.
-   Server-side validation and rate limiting were not verified.
-   Multi-user authorization and session isolation were not tested.
-   A complete dependency inventory was unavailable.
-   CSP and CORS observations were inconsistent and need direct
    confirmation.
-   Dynamic injection, load, and error-condition testing were not
    performed.

## 3. OWASP Top 10:2025 checklist

Status reflects the evidence recorded in the original assessment, not a
claim that the application is secure.

  -----------------------------------------------------------------------
  OWASP category          Status                  Summary
  ----------------------- ----------------------- -----------------------
  A01: Broken Access      Not tested              Public pages were
  Control                                         visible. Authorization
                                                  boundaries and result
                                                  ownership were not
                                                  verified.

  A02: Security           Follow-up required      Several security
  Misconfiguration                                headers were reported
                                                  present. CSP and CORS
                                                  observations were
                                                  inconsistent.

  A03: Software Supply    Partially reviewed      Zod was identified, but
  Chain Failures                                  dependency versions and
                                                  the full dependency
                                                  tree were unavailable.

  A04: Cryptographic      Partially reviewed      HTTPS-related
  Failures                                        protections were
                                                  reported by the scan.
                                                  Sensitive-data storage
                                                  and handling were not
                                                  assessed.

  A05: Injection          Partially reviewed      Client-side Zod
                                                  validation was visible.
                                                  Server-side validation
                                                  and safe output
                                                  handling were not
                                                  verified.

  A06: Insecure Design    Not tested              Rate limiting and abuse
                                                  controls could not be
                                                  confirmed.

  A07: Authentication     Not tested              No login flow was
  Failures                                        visible in the reviewed
                                                  public UI. The need for
                                                  authentication and any
                                                  backend session
                                                  controls remain
                                                  unclear.

  A08: Software or Data   Partially reviewed      Zod was identified, but
  Integrity Failures                              dependency integrity,
                                                  build controls, and
                                                  external script
                                                  protections were not
                                                  fully assessed.

  A09: Security Logging   Not tested              Server-side logs and
  and Alerting Failures                           alerts were not
                                                  accessible for review.

  A10: Mishandling of     Partially reviewed      No obvious verbose
  Exceptional Conditions                          errors were reported in
                                                  the normal UI. Error
                                                  paths were not
                                                  deliberately tested.
  -----------------------------------------------------------------------

## 4. Key observations

### 4.1 HTTP security headers

The assessment records a SecurityHeaders.com grade of A on 27 October
2026. It reports these headers as present:

-   Strict-Transport-Security (HSTS)
-   X-Content-Type-Options
-   X-Frame-Options
-   Referrer-Policy
-   Permissions-Policy

The assessment also records uncertainty about whether a
Content-Security-Policy header is actually present. Re-run the scan and
inspect the raw response headers before treating this as a confirmed
issue.

**Next step:** Save a screenshot or export of the scan and record the
date, grade, and exact header values.

### 4.2 CORS configuration

The original assessment reports `Access-Control-Allow-Origin: *`
alongside `Access-Control-Allow-Credentials: true`. If those values are
genuinely returned together, the configuration should be reviewed. The
original assessment could not confirm whether the observed response
reflects the effective application policy.

**Next step:** Ask the platform provider to confirm the effective CORS
configuration for `/api/intake`. Do not label this a confirmed
exploitable vulnerability without further evidence.

### 4.3 Input validation

The client-side form uses Zod validation and field-length constraints.
This is useful, but client-side checks can be bypassed. The assessment
did not inspect or test the backend validation logic.

**Next step:** Confirm that the server independently validates input
length, type, and format, and that it safely handles user input before
storing, processing, or rendering it.

### 4.4 Rate limiting and abuse prevention

The assessment did not establish whether `/api/intake` has rate limits.
The absence of visible rate-limit headers in a normal request does not
prove that rate limiting is missing.

**Next step:** Confirm the configured limits with the platform provider
or test them in an approved staging environment.

### 4.5 Dependencies and integrity

Zod was identified, but the complete dependency list and package
versions were unavailable. The assessment therefore could not establish
whether dependencies are vulnerable or whether external scripts use
Subresource Integrity.

**Next step:** If source and package lock files are available, run a
dependency audit and review any reported vulnerabilities. Do not claim a
dependency is vulnerable without a version-specific result.

### 4.6 Logging and error handling

Server-side logs and alerting were not available for review. The normal
user interface reportedly did not expose obvious verbose errors, but
failure cases were not tested.

**Next step:** Confirm that detailed errors are logged securely on the
server while users receive generic error messages that do not reveal
secrets, stack traces, or internal paths.

## 5. Prioritized action plan

  -----------------------------------------------------------------------
  Priority                Action                  Owner to confirm
  ----------------------- ----------------------- -----------------------
  1                       Verify the actual CSP   Polsia/platform
                          and CORS response       
                          headers.                

  2                       Confirm server-side     Application
                          validation and safe     team/platform
                          output handling for     
                          `/api/intake`.          

  3                       Confirm rate limiting   Polsia/platform
                          and abuse controls for  
                          `/api/intake`.          

  4                       Obtain a dependency     Application
                          inventory and audit     team/platform
                          package versions.       

  5                       Confirm access-control  Application
                          expectations for        team/platform
                          results and any API     
                          endpoints.              

  6                       Review server-side      Application
                          error handling,         team/platform
                          logging, and alerting.  
  -----------------------------------------------------------------------

Ownership is provisional. Confirm which settings Polsia manages and
which can be changed by the application owner.

## 6. Retesting plan

After fixes or confirmations:

1.  Re-run SecurityHeaders.com and save the results.
2.  Record the exact CSP and CORS response headers.
3.  Verify server-side input validation in an approved test environment.
4.  Confirm rate limiting without sending disruptive traffic.
5.  Audit dependencies when the package manifest and lock file are
    available.
6.  Record each result as **Verified**, **Failed**, **Not Tested**, or
    **Not Applicable**, with evidence and a test date.

## 7. Conclusion

The review identified useful areas for follow-up, particularly
clarification of CSP and CORS, server-side validation, rate limiting,
and dependency visibility. The available evidence is not sufficient to
conclude that these are all exploitable vulnerabilities or that the
application is secure.

The next step is to validate the uncertain observations, fix confirmed
issues, and update this report with evidence from retesting.

## References

-   OWASP Top 10:2025: https://owasp.org/Top10/2025/
-   OWASP Web Security Testing Guide:
    https://owasp.org/www-project-web-security-testing-guide/
-   SecurityHeaders.com: https://securityheaders.com/

------------------------------------------------------------------------

**Portfolio note:** This report documents a limited, read-only
assessment. It does not claim a full penetration test, and unverified
observations are explicitly marked for follow-up.
