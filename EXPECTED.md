# Expected outcomes — bump-it wrapper

Baseline expectations written 2026-10-10 for supply-chain 0.3.0 and updated
2026-10-12: main's wrapper is Gradle 9.8.0, the gate is pinned to v0.4.0 and the
tools are at v0.4.2.

| Case | Files | bump-it | secure-it | Acceptance |
|---|---|---|---|---|
| Wrapper routine | gradlew, gradlew.bat, gradle/wrapper/gradle-wrapper.jar, gradle/wrapper/gradle-wrapper.properties | From main's 9.8.0, choose the highest eligible aged stable non-broken Gradle release under the live advisory snapshot: a release in the same major line goes in the routine, a newer major in its own PR. Replace all four tool-generated files and verify official checksums and executable mode. | No Gradle-wrapper remediation mechanism; no A/B/C project-dependency case is seeded here. | ./gradlew check --no-daemon passes. Wrapper bytes/modes match the plan's generated files. Any Gradle verification uses a reference with the planned wrapper overlay. |
| Historical run | Same files | On 2026-10-07 bump-it selected 9.8.0 from the 9.7.1 seed (PR #1, merged 2026-10-08); see VALIDATION.md. That seed is consumed. To run from 9.7.1 again, restore the four wrapper files as they were at 63a03f8. | No fixed security unit expected. | Do not freeze selection to a historical target after a newer eligible release ages. |

This fixture remains dependency-free. Do not add npm or Gradle module dependencies
merely to accommodate carrier or parent remediation tests. It does have a
supply-chain gate workflow (`.github/workflows/supply-chain.yml:16`, pinned to
v0.6.0); a bump-it routine may move that pin like any own Action. Retain the
selected catalog release, plan, generated wrapper hashes/modes, verification and
CI evidence, and record each run in VALIDATION.md.
