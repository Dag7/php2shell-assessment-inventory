# PHP assessment inventory

This repository contains an assessment scaffold and a small passive PHP technology inventory. **No sites have been assessed or directly probed.** The Ora configuration in `autopilot/` describes a bounded hosted review; it does not implement a scanner or scheduled assessment.

The PHP2Shell advisories cover [CVE-2026-109618](https://github.com/php/php-src/security/advisories/GHSA-w8hw-w9fx-j79w) and [CVE-2026-109619](https://github.com/php/php-src/security/advisories/GHSA-6wmf-4rv5-p3rp). PHP lists upstream fixes in 8.2.35, 8.3.36, 8.4.27, and 8.5.12 in its [2026 release archive](https://www.php.net/archive/2026.php). Assess each CVE's applicability and vendor patch evidence separately.

## Start with scope

Record explicitly approved hosts in `scope.json` before directly collecting site observations. Its empty `allowed_hosts` list currently authorizes no direct assessment or probing. Each entry must contain:

| Field | Required value |
| --- | --- |
| `host` | One exact hostname; no wildcard, network range, or automatic expansion. |
| `permission_reference` | Reference to the owner's permission or the applicable assessment agreement. |
| `expires_at` | Expiration time in RFC 3339 format, including timezone. |
| `allowed_methods` | Explicit approved methods, such as owner-provided runtime inspection or limited HTTP header retrieval. |
| `request_budget` | Object with `max_requests` and `max_requests_per_minute`, both positive integers; counts apply across all workers for that host. |

An expired or incomplete entry grants no scope. A redirect, related hostname, shared IP address, or linked site does not extend permission. Scope changes require an explicit user instruction identifying the approved host and permission reference.

## Passive batch 001

The user requested technology profiling sources and a limited number of domains. `research/passive-batch-001.json` records five hostnames from Wappalyzer's public PHP sample, in their published order. The batch is capped at five candidate domains. BuiltWith and PublicWWW were also reviewed as source options; no paid exports were purchased and no source restrictions were bypassed.

These are third-party technology claims, with no per-site PHP version or patch evidence. Each candidate's PHP2Shell CVE status is `unknown`. A candidate is not an active assessment target, a vulnerability finding, or evidence that its owner should receive a vulnerability alert. No direct requests were sent to the five candidate hostnames, and `data/observations.jsonl` remains empty.

## Record evidence

Store one observation per line in `data/observations.jsonl`, following `schemas/observation.schema.json` (JSON Schema draft 2020-12). Each observation includes the asset hostname, observation timestamp, permission reference, PHP details, evidence references and collection timestamps, a separate assessment for each relevant CVE, each with its own evidence, status, and rationale. Owner runtime evidence must identify the runtime instance with `runtime_instance_id`. Store references and concise summaries rather than credentials, cookies, raw response bodies, or raw logs.

The PHP record captures the observed runtime version, optional package/build details, and whether backport status is known. Public banners and headers can be absent, stale, or misleading. A version header alone cannot confirm vulnerability. Distribution backports and vendor patch levels can change whether a build is affected; an upstream version number is insufficient by itself.

| Status | Meaning |
| --- | --- |
| `unknown` | Evidence is insufficient to assess the relevant CVEs. |
| `suspected_affected_version` | Available version evidence suggests an affected version; build applicability and other conditions remain unconfirmed. |
| `affected_build_confirmed` | Owner-provided runtime or patch evidence establishes an affected build and the advisory's applicable conditions; rationale must identify both. This does not claim successful exploitation. |
| `fix_verified` | Owner evidence establishes the relevant fix, including vendor backports where applicable. Runtime evidence must identify the serving instance and verify `runtime_serving_traffic: true` and `workers_restarted: true`; rationale must identify the verification basis. |

The schema requires owner runtime or patch evidence for `affected_build_confirmed` and `fix_verified`; a header-only record fails validation for either status. A missing banner or a banner reporting a fixed version does not verify a fix. No status establishes remote exploitability. An evidence category is a provenance assertion, so reviewers must verify its source and content. Match current primary advisories to the deployment conditions before choosing a status. Keep unverified findings marked accordingly.

## Validation and repository

Parse `scope.json`, the schema, and every nonempty JSONL line as JSON. Validate each observation with a validator supporting draft 2020-12 and date-time/hostname format checking. Review each host's permission, expiration, methods, and remaining request budget before any permitted collection.

The public repository is [Dag7/php2shell-assessment-inventory](https://github.com/Dag7/php2shell-assessment-inventory). It was made public with the owner's approval for credential-free hosted reads. Hosted agents receive no GitHub write credential; the operator reviews and pushes their report. Review changes for sensitive information before committing and pushing. The initial files parse as JSON; a full draft-2020-12 schema validator was not run. Consult `setup-status.json` for the verified setup state and `advisory.json` for dated advisory facts and primary sources.

Consult `autopilot/README.md` and the recorded runtime state before asserting that a team or mission is running. Do not publish vulnerability findings automatically or contact asset owners from this inventory.
