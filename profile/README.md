<p align="center">
  <img align="center" src="https://cdn.metorial.com/2025-06-13--14-59-55/logos/metorial/primary_logo/raw.svg" alt="Metorial" width="70px" />
</p>

<h1 align="center">Metorial</h1>

<p align="center">
Open-source identity and access layer for AI agents.
</p>

## Why Metorial?

Agents are being connected to production systems, but without a consistent identity and access layer around them; 
limited access control, no auditing, no access restrictions. 
Metorial solves that.

## What we're building

Metorial is a control plane for agent access to external systems.
It sits between agents and integrations, handling auth, permissions, and observability in a consistent way.
Instead of wiring integrations ad hoc, teams get a shared layer that standardizes how agents interact with systems.

Core capabilities:

- 1200+ integrations
- support for custom integrations and MCP servers  
- auth and token lifecycle management  
- RBAC, SAML SSO, and IAM built-in  
- scoped permissions per agent, workflow, or team  
- audit logs and traceability for agent actions  
- shared access patterns across teams and projects  

### Metorial for Developers

Metorial gives developers a single interface for connecting agents to real systems.

- use integrations across tools like Claude Code, Codex, and Cursor without breaking security policies  
- expose integrations as tools to any agent framework  
- unify OAuth, API keys, and other auth flows into one magic URL
- reuse connections across projects, environments, and people
- avoid re-implementing messy integration and auth logic

You write against one API, or use one connection URL and Metorial handles the rest.

### Metorial for Security

Metorial provides structure and visibility into how agents access systems.

- centralized access control (RBAC, SAML SSO, IAM, the entire alphabet)  
- clear permission boundaries per agent  
- audit logs for all actions, including which agent performed them using whose credentials
- controlled sharing of integrations  
- consistent and secure credential handling  

This makes agent activity enforceable and inspectable without relying on manual processes. 
Makes your Head of AI happy, lets your CISO sleep at night.

## Ecosystem

* [Metorial](https://github.com/metorial/metorial): Integration catalog covering SaaS tools and enterprise systems  
* [Metorial Platform](https://github.com/metorial/metorial-platform): Core engine, open source and self-hostable  
* [Metorial CLI](https://github.com/metorial/cli): Agent-first CLI for interacting with integrations  
* [Lowerdeck](https://github.com/metorial/lowerdeck): Shared libraries across the stack  
* [Starbase](https://github.com/metorial/starbase): MCP debugging and testing utility  

## SDKs

The SDKs expose the Metorial API and integrate with agent frameworks.

They handle auth, access control, and tool exposure in a consistent way.

* <img src="https://raw.githubusercontent.com/metorial/metorial-platform/refs/heads/dev/assets/typescript.png" width="12px" height="12px" /> [**JavaScript / TypeScript**](https://github.com/metorial/metorial-node)  
* <img src="https://raw.githubusercontent.com/metorial/metorial-platform/refs/heads/dev/assets/python.svg" width="12px" height="12px" /> [**Python**](https://github.com/metorial/metorial-python)  

Example: create an OAuth flow for Slack and expose it as tools to an agent (here using Vercel AI SDK):

### JavaScript / TypeScript

```ts
let setupSession = await metorial.providerDeployments.setupSessions.create({
  providerId: "slack",
  providerAuthMethodId: "oauth",
});

console.log(setupSession.url);

let session = await metorial.connect({
  adapter: metorialAiSdk(),
  providers: [
    {
      providerDeploymentId: "slack-deployment-id",
      providerAuthConfigId: "auth-config-id",
    },
  ],
});

console.log(session.tools())
```
