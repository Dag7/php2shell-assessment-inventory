# Ora production configuration

Ora CLI 0.13.0 authenticates against `https://api.agentfront.sh` using an externally supplied API key. Production authentication, Autopilot permissions, the strategy catalog, and the three hosted harness/model offerings were verified on October 25, 2026. No key or token is stored in this repository.

| Member | Harness | Offered model |
| --- | --- | --- |
| Coordinator and maintainer | `codex` | `gpt-6.1-sol` |
| Advisory researcher | `claude-code` | `claude-opus-5-5` |
| Independent reviewer | `opencode` | `claude-sonnet-5-5` |

`team.json` is the resolved team request. `team.template.json` preserves the original unresolved draft and must not be submitted. The configuration requests a $5 mission cap, 12 turns, 10 minutes, and stop on a budget trip. Dollar accounting is a reported, soft limit; the time and turn limits are the backstops. No nested worker spawning is permitted.

`mission.json` is a single passive review of the existing five-domain technology inventory. It permits requests to the named profiling services and primary advisory sources, with zero requests to candidate hosts. It does not launch a scanner, CVE test, owner outreach, or recurring process.

The repository is public so hosted workers can clone it without GitHub credentials. They prepare a structured review and publish its complete JSON in a team note titled `passive-batch-001-review`. The operator inspects and pushes that result using the existing local GitHub connection. No GitHub write token is provided to hosted workers.

Inspect the actual state after authentication:

```sh
ora autopilot teams get php-inventory-review --api-url https://api.agentfront.sh --json
ora autopilot missions list php-inventory-review --api-url https://api.agentfront.sh --json
ora autopilot notes list php-inventory-review --api-url https://api.agentfront.sh --json
```

See `setup-status.json` for the last verified runtime state. A resolved request does not prove successful provisioning or execution. The [public OpenAPI document](https://api.agentfront.sh/openapi.json) and [official CLI documentation](https://www.npmjs.com/package/@ora-ai/cli) describe the API and authentication requirements.
