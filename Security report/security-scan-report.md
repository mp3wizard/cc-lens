# Automated Security Scan Report

**Target:** `/Users/mp3wizard/Public/Claude Code Lens/cc-lens`
**Scanned at:** 2026-04-07T09:41:00+07:00
**Triggered by:** Upstream sync — merged commits `6156b55`, `3c351b7` (v0.2.9 → v0.2.10)
**Tools run:** Gitleaks, Semgrep (OWASP Top 10, TypeScript, Secrets), Trivy, TruffleHog, OSV-Scanner
**Tools skipped:** Bandit (no project `.py` files), CodeQL (no workflow in repo), mcps-audit (no MCP files), mcp-scan (opt-in only)

---

## Pre-flight Summary

| Tool        | Status  | Version / Note                                  |
|-------------|---------|--------------------------------------------------|
| Gitleaks    | OK      | 8.30.1                                           |
| Bandit      | SKIPPED | No project Python files (only in node_modules)  |
| Semgrep     | OK      | 1.157.0                                          |
| Trivy       | OK      | 0.69.3 — not in compromised range               |
| TruffleHog  | OK      | 3.94.2                                           |
| CodeQL      | N/A     | No `.github/workflows/codeql.yml` found         |
| mcps-audit  | N/A     | No MCP skill/config files in project            |
| OSV-Scanner | OK      | 2.3.5                                            |
| mcp-scan    | OPT-IN  | Not run — user opt-in required                  |

---

## Gitleaks — Secrets in Git History & Filesystem

**Summary:** 0 findings

```
28 commits scanned.
scanned ~857717 bytes (857.72 KB) in 99.8ms
no leaks found
```

---

## Semgrep — Multi-language SAST

### OWASP Top 10
**Summary:** 0 findings

```
Scanning 86 files tracked by git with 544 Code rules:
Ran 77 rules on 86 files: 0 findings.
```

### TypeScript
**Summary:** 0 findings

```
Scanning 85 files tracked by git with 74 Code rules:
Ran 74 rules on 85 files: 0 findings.
```

### Secrets
**Summary:** 0 findings

```
Scanning 102 files tracked by git with 52 Code rules:
Ran 41 rules on 102 files: 0 findings.
Note: 3 files skipped (>300 KB limit)
```

---

## Trivy — Dependencies, IaC, Secrets

**Summary:** 0 findings

```
Report Summary
┌───────────────────┬──────┬─────────────────┬─────────┐
│      Target       │ Type │ Vulnerabilities │ Secrets │
├───────────────────┼──────┼─────────────────┼─────────┤
│ package-lock.json │ npm  │        0        │    -    │
└───────────────────┴──────┴─────────────────┴─────────┘
```

---

## TruffleHog — Secrets in Git History (with live verification)

**Summary:** 0 verified secrets, 0 unverified secrets

```
chunks: 638, bytes: 870772
verified_secrets: 0, unverified_secrets: 0
scan_duration: 280ms
```

---

## OSV-Scanner — SCA Dependency Vulnerabilities

**Summary:** 1 Medium vulnerability found — **0 fixable**

```
Total 1 package affected by 1 known vulnerability
(0 Critical, 0 High, 1 Medium, 0 Low, 0 Unknown)
0 vulnerabilities can be fixed.

+-------------------------------------+------+-----------+---------+---------+---------------+-------------------+
| OSV URL                             | CVSS | ECOSYSTEM | PACKAGE | VERSION | FIXED VERSION | SOURCE            |
+-------------------------------------+------+-----------+---------+---------+---------------+-------------------+
| https://osv.dev/GHSA-5f7q-jpqc-wp7h | 5.9  | npm       | next    | 16.2.2  | --            | package-lock.json |
+-------------------------------------+------+-----------+---------+---------+---------------+-------------------+
```

### GHSA-5f7q-jpqc-wp7h — Next.js Unbounded Memory Consumption via PPR Resume Endpoint

- **Severity:** Medium (CVSS 3.1: AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:N/A:H — score 5.9)
- **Package:** `next` v16.2.2
- **Fixed version:** None available (16.2.2 is the latest)
- **Description:** DoS vulnerability affecting Next.js with Partial Prerendering (PPR) enabled in minimal mode. The PPR resume endpoint accepts unauthenticated POST requests with the `Next-Resume: 1` header and processes attacker-controlled postponed state data, allowing memory exhaustion and server crash.
- **Exploitability:** AC:H (High complexity — requires PPR enabled in minimal/standalone mode)
- **Impact to cc-lens:** cc-lens is a local desktop/developer tool, not a production server exposed to the internet. PPR is not documented as enabled in this project's Next.js config.
- **Status:** UNFIXABLE — no patched version exists in the 16.x branch as of 2026-04-07.
- **Recommendation:** Monitor upstream Next.js releases for a fix. If PPR is not used, the attack surface is not present.

---

## Cross-Tool Observations

No cross-tool overlaps detected. All SAST and secret-scanning tools returned clean results. The single OSV finding is a dependency vulnerability with no available fix.

## Coverage Gaps

| Category | Gap |
|----------|-----|
| Business logic / IDOR | Not covered by any automated tool — requires manual review |
| Runtime behavior | Static analysis only; dynamic/fuzzing not performed |
| CodeQL deep SAST | No `.github/workflows/codeql.yml` — add for semantic analysis coverage |
| mcp-scan | Opt-in not exercised — MCP tool poisoning/prompt injection not assessed |

---

## Remediation Summary

| Finding | Severity | Fixed | Reason |
|---------|----------|-------|--------|
| GHSA-5f7q-jpqc-wp7h (next v16.2.2) | Medium | No | No patched version exists; 16.2.2 is latest |

**Fixed: 0 | Unfixable: 1**

No version bump applied (no security fixes committed).
