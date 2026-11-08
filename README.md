# GitHub MCP server

Identify your account, then list a chosen repository’s issues for a daily triage brief.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `GITHUB_TOKEN`



Credential help: https://raw.githubusercontent.com/github/rest-api-description/main/descriptions/api.github.com/api.github.com.yaml

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call get_authenticated_user '{}'
```

## Use with an MCP client

Launch `node /absolute/path/github-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| get_authenticated_user | Read | Read the authenticated GitHub user. |
| list_repository_issues | Read | List repository issues and pull requests visible to your token. |
| create_issue | Explicit approval required | Create a repository issue only after explicit per-call approval. |

## Concrete workflow

Identify your account, then list a chosen repository’s issues for a daily triage brief.

1. get_authenticated_user
2. list_repository_issues

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=github&integration=github-mcp&utm_source=github&utm_campaign=github-github-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/github/).

## Provenance and maintenance

- https://docs.github.com/en/rest/issues/issues

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
