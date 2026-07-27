---
name: Isolate and release a compromised endpoint
description: Find an agent, isolate its host from the network to contain a threat, then release isolation once remediated.
api: openapi/huntress-rest-openapi.json
operations: [getV1Agents, getV1AgentsId, IsolateAgent, ReleaseAgent]
---

# Isolate and release a compromised endpoint

Authenticate with HTTP Basic (API key + secret) against `https://api.huntress.io/v1`.

1. **Locate the agent** — `getV1Agents` (`GET /v1/agents`), cursor-paginated with
   `limit` + `page_token`. Confirm the target with `getV1AgentsId`
   (`GET /v1/agents/{id}`).
2. **Isolate the host** — `IsolateAgent`
   (`POST /v1/agents/{id}/isolation`). This is a safety-critical, containing action;
   confirm intent before calling.
3. **Release isolation** once the host is remediated — `ReleaseAgent`
   (`DELETE /v1/agents/{id}/isolation`).

Error rules: `409` = the agent does not support host isolation, or isolation could
not be scheduled — surface the message, do not blind-retry. `403` = credential/
permission issue; `404` = agent not found. See conventions/huntress-conventions.yml
and errors/huntress-problem-types.yml.
