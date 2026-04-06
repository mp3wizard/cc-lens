# Automated Security Scan Report
**Target:** `/Users/mp3wizard/Public/cc-lens`  **Scanned at:** 2026-04-05T17:05:39Z
**Tools run:** Gitleaks, Semgrep (OWASP Top 10, TypeScript, Secrets), Trivy, TruffleHog, OSV-Scanner
**Tools skipped:** Bandit (no .py files), CodeQL (no `.github/workflows/codeql.yml`), mcps-audit (no MCP files), mcp-scan (opt-in only)

---

## Pre-flight Summary

| Tool         | Status  | Version / Note                                      |
|--------------|---------|-----------------------------------------------------|
| Gitleaks     | OK      | 8.30.1                                              |
| Bandit       | SKIPPED | No `.py` files found                                |
| Semgrep      | OK      | 1.157.0                                             |
| Trivy        | OK      | 0.69.3 (not in compromised range)                   |
| TruffleHog   | OK      | 3.94.2                                              |
| CodeQL       | N/A     | GitHub repo, but no `codeql.yml` workflow present   |
| mcps-audit   | SKIPPED | No MCP skill/config files found                     |
| OSV-Scanner  | OK      | 2.3.5                                               |
| mcp-scan     | OPT-IN  | Not run — requires user consent (sends data to invariantlabs.ai) |

---

## Gitleaks — Secrets in Git History

**Summary:** 0 findings across 25 commits (~846 KB scanned in 130ms)

```
12:04AM INF 25 commits scanned.
12:04AM INF scanned ~846079 bytes (846.08 KB) in 130ms
12:04AM INF no leaks found
```

---

## Semgrep — Multi-language SAST

### OWASP Top 10
**Summary:** 0 findings — 77 rules on 86 files (TypeScript + JS)

```
✅ Scan completed successfully.
 • Findings: 0 (0 blocking)
 • Rules run: 77
 • Targets scanned: 86
 • Parsed lines: ~100.0%
```

### TypeScript Rules
**Summary:** 0 findings — 74 rules on 85 files

```
✅ Scan completed successfully.
 • Findings: 0 (0 blocking)
 • Rules run: 74
 • Targets scanned: 85
```

### Secrets
**Summary:** 0 findings — 41 rules on 101 files (3 files skipped: >300 KB)

```
✅ Scan completed successfully.
 • Findings: 0 (0 blocking)
 • Rules run: 41
 • Targets scanned: 101
 • Scan skipped: Files larger than 0.3 MB: 3
```

---

## Trivy — Dependencies, Secrets, IaC

**Summary:** 0 vulnerabilities, 0 secrets

```
Report Summary
┌───────────────────┬──────┬─────────────────┬─────────┐
│      Target       │ Type │ Vulnerabilities │ Secrets │
├───────────────────┼──────┼─────────────────┼─────────┤
│ package-lock.json │ npm  │        0        │    -    │
└───────────────────┴──────┴─────────────────┴─────────┘
```

---

## TruffleHog — Git History Secrets (with Live Verification)

**Summary:** 0 verified secrets, 0 unverified secrets across 593 chunks (857 KB)

```
2026-04-05T17:04:59Z  info  scanning repo: file:///Users/mp3wizard/Public/cc-lens
2026-04-05T17:04:59Z  info  finished scanning  {
  "chunks": 593, "bytes": 857920,
  "verified_secrets": 0, "unverified_secrets": 0,
  "scan_duration": "265.183959ms"
}
```

---

## OSV-Scanner — Dependency Vulnerabilities (SCA)

**Summary:** ⚠️ **17 known vulnerabilities in 10 packages** — 0 Critical, **8 High**, 9 Medium, 0 Low
16 of 17 have available fixes. **1 has no fix** (`next` 16.2.2).

```
+-------------------------------------+------+-----------+--------------------------+---------+---------------+
| OSV URL                             | CVSS | ECOSYSTEM | PACKAGE                  | VERSION | FIXED VERSION |
+-------------------------------------+------+-----------+--------------------------+---------+---------------+
| GHSA-rf6f-7fwh-wjgh (flatted)       | 8.9  | npm       | flatted                  | 3.3.3   | 3.4.2         |  ← Highest CVSS
| GHSA-wc8c-qw6v-h7f6 (@hono/node-s.) | 7.5  | npm       | @hono/node-server (dev)  | 1.19.9  | 1.19.10       |
| GHSA-46wh-pxpv-q5gq (express-r-l.)  | 7.5  | npm       | express-rate-limit (dev) | 8.2.1   | 8.2.2         |
| GHSA-25h7-pfq9-p65f (flatted)       | 7.5  | npm       | flatted                  | 3.3.3   | 3.4.0         |
| GHSA-q5qw-h33p-qvwr (hono)          | 7.5  | npm       | hono (dev)               | 4.12.3  | 4.12.4        |
| GHSA-j3q9-mxjg-w52f (path-to-regexp)| 7.5  | npm       | path-to-regexp (dev)     | 8.3.0   | 8.4.0         |
| GHSA-c2c7-rcm5-vvqj (picomatch)     | 7.5  | npm       | picomatch (dev)          | 2.3.1   | 2.3.2         |
| GHSA-c2c7-rcm5-vvqj (picomatch)     | 7.5  | npm       | picomatch (dev)          | 4.0.3   | 4.0.4         |
| GHSA-f886-m6hf-6m8v (brace-exp.)    | 6.5  | npm       | brace-expansion (dev)    | 1.1.12  | 1.1.13        |
| GHSA-f886-m6hf-6m8v (brace-exp.)    | 6.5  | npm       | brace-expansion (dev)    | 5.0.4   | 5.0.5         |
| GHSA-p6xx-57qc-3wxr (hono)          | 6.5  | npm       | hono (dev)               | 4.12.3  | 4.12.4        |
| GHSA-5f7q-jpqc-wp7h (next)          | 5.9  | npm       | next                     | 16.2.2  | NO FIX        |  ← No fix available
| GHSA-27v5-c462-wpq7 (path-to-regexp)| 5.9  | npm       | path-to-regexp (dev)     | 8.3.0   | 8.4.0         |
| GHSA-5pq2-9x2x-5p6w (hono)          | 5.4  | npm       | hono (dev)               | 4.12.3  | 4.12.4        |
| GHSA-3v7f-55p6-f55p (picomatch)     | 5.3  | npm       | picomatch (dev)          | 2.3.1   | 2.3.2         |
| GHSA-3v7f-55p6-f55p (picomatch)     | 5.3  | npm       | picomatch (dev)          | 4.0.3   | 4.0.4         |
| GHSA-v8w9-8mx6-g223 (hono)          | 4.8  | npm       | hono (dev)               | 4.12.3  | 4.12.7        |
+-------------------------------------+------+-----------+--------------------------+---------+---------------+
```

### Remediation
Most affected packages are **dev dependencies** and can be updated via `npm update` or by bumping versions in `package.json`:
- `flatted` → `>= 3.4.2`
- `@hono/node-server` → `>= 1.19.10`
- `hono` → `>= 4.12.7`
- `path-to-regexp` → `>= 8.4.0`
- `picomatch` → `>= 2.3.2` / `>= 4.0.4`
- `brace-expansion` → `>= 1.1.13` / `>= 5.0.5`
- `express-rate-limit` → `>= 8.2.2`
- `next` → **No fix available** (GHSA-5f7q-jpqc-wp7h, CVSS 5.9) — monitor upstream

---

## CodeQL — Deep Semantic SAST

**Summary:** SKIPPED — GitHub repo confirmed (`https://github.com/Arindam200/cc-lens`) but no `codeql.yml` workflow found in `.github/workflows/`. This is a coverage gap for deep data-flow analysis.

---

## Cross-Tool Observations

No cross-tool overlaps detected for secrets or SAST findings. The only findings are dependency vulnerabilities reported by OSV-Scanner. Trivy's npm scan (0 findings) and OSV-Scanner's results differ because Trivy suppresses dev dependencies by default — OSV-Scanner surfaces them, revealing the 17 vulnerabilities.

---

## Coverage Gaps

| Category              | Gap Detail |
|-----------------------|------------|
| Business logic flaws  | Not covered by any automated tool |
| IDOR / authorization  | Requires runtime/manual testing   |
| CodeQL deep SAST      | No codeql.yml workflow; add to repo for data-flow analysis |
| mcp-scan              | Opted out — MCP prompt injection not assessed |
| 3 files >300 KB       | Skipped by Semgrep secrets scan (size limit) |
| Runtime behavior      | Only static analysis was performed |
