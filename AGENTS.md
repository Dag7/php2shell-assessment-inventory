# Assessment boundaries

- No direct site assessment or probe is authorized by this repository while `scope.json` has an empty `allowed_hosts` list.
- The user requested a limited review of published technology profiles. Batch 001 permits passive research on at most five candidate hostnames using BuiltWith, Wappalyzer, and PublicWWW. Store this in `research/`; it does not add hosts to the active scope or establish a vulnerability. Do not expand or repeat the batch autonomously.
- Collect only for exact hosts explicitly approved by the user and recorded with `host`, `permission_reference`, unexpired `expires_at`, `allowed_methods`, and a shared `request_budget` containing `max_requests` and `max_requests_per_minute`.
- Do not add targets through autonomous discovery. Redirects, related domains, shared addresses, search results, and links do not extend scope. Ask for missing host or permission details before collecting.
- Stay within the approved methods and request budgets across all workers. Do not send exploit payloads, perform overload probes, or attempt exploitation.
- Record concise evidence references and collection timestamps. Do not store credentials, cookies, raw response bodies, or raw logs. Follow the observation schema.
- Headers or banners alone cannot establish an affected build or a verified fix. Use separate assessments per CVE. Require owner runtime or patch evidence and account for vendor backports and advisory conditions before those statuses. Owner runtime evidence must identify `runtime_instance_id`; `fix_verified` also requires verified evidence that the runtime is serving traffic and its workers were restarted. A missing or fixed-version banner never suffices. No status establishes remote exploitability.
- Do not send outbound owner messages or automatically publish findings. Do not push to an unapproved destination.
- Do not claim that a Claude, Codex, or OpenCode team is running without implemented integrations and verified execution. This scaffold has no CI, runner, or production deployment.
