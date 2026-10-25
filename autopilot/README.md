# Ora setup draft

Ora CLI 0.13.0 is installed locally. The setup check returned `No api key configured`; no Ora team or mission has been created. These JSON files describe a bounded passive review, not a vulnerability scanner. The team template deliberately contains unresolved model, harness, and repository-secret fields. Do not submit it before resolving them.

The request structure was checked against [Ora's public OpenAPI document](https://api.agentfront.sh/openapi.json) on October 25, 2026. See the [official CLI package documentation](https://www.npmjs.com/package/@ora-ai/cli) for authentication and scope requirements.

## Authenticate and resolve the configuration

Run login in a trusted terminal and enter the key at its masked prompt; do not put API keys into chat, this repository, or command-line arguments:

```sh
ora login --api-url https://api.agentfront.sh
ora whoami --api-url https://api.agentfront.sh --json
ora sessions catalog --api-url https://api.agentfront.sh --json
ora autopilot strategies list --api-url https://api.agentfront.sh --json
```

The key needs access to the `experiment` product, `autopilot:read`, `autopilot:write`, and `sessions:read`. Binding a repository credential additionally requires `secrets:bind` and an eligible organization role. Verify actual permissions after login.

Select the exact Claude, Codex, and OpenCode harness/model combinations from the offered catalog. Confirm all three are eligible for standing teams. Local CLI logins and a locally missing OpenCode binary do not establish hosted Ora availability. Do not substitute an unverified model or silently omit a requested member.

Configure a GitHub credential in Ora with access to this repository, and replace the secret-reference placeholder with its reference, never the secret value. Local `gh` credentials are not automatically credentials for hosted workers. A public repository could permit unauthenticated reads, but pushes still require a write credential. Repo visibility does not resolve the missing Ora API key.

Save the resolved request as `autopilot/team.json` and only then create the team and run its single passive mission:

```sh
ora autopilot teams create --api-url https://api.agentfront.sh --file autopilot/team.json --json
ora autopilot missions create php-inventory-review --api-url https://api.agentfront.sh --file autopilot/mission.json --watch
```

Verify the created roster, applied models, cloned repository, mission state, resulting commit, and final stop state. The draft sets a $5 mission cap, 12 turns, and 10 minutes, with stop on a budget trip. These are limits requested by the configuration, not a claim that a running service has applied them. No production operation has been verified.
