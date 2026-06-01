---
name: alejo-secrets-v2
description: Compact Alejo Secrets v2 workflow for setting up required API keys, credentials, provider resources, public config, and runtime environment variables in Doppler for Alejo Linear Project Documents, implementation issues, Alejo Run, and production slices. Use when secrets or provider resources must be found, reused, created after plan verification, safely recovered into Doppler, or handed to the human only when truly required.
---

# Alejo Secrets v2

Set up required runtime secrets and provider config in Doppler. Prefer automatic discovery, safe recovery, and verified resource creation. Ask the human only for values or provider choices Codex cannot obtain, create, or disambiguate safely.

Never ask the user to paste secret values into Codex, chat, files, logs, or code. Never write `.env`, inventories, local mirrors, or secret artifact files.

## Sources

Use Linear Project Documents, Linear issues, and current repo evidence:

1. Current request and supplied issue refs.
2. `AGENTS.md`: project orientation and source-of-truth map.
3. `SAD.xml` or `SAT.xml`: providers, deployment, security, operations, and required config.
4. `PRD.xml`, `Q&A.xml`, `CONTEXT.xml`, `prototype.xml`, and ADR XML documents when they affect providers, scopes, environments, or runtime behavior.
5. Linear implementation issues, run contracts, comments, and review gaps.
6. Current codebase: env examples, config loaders, provider adapters, deployment config, CI, tests, and runtime commands.
7. Authenticated provider accounts through official CLIs, MCP connectors, APIs, dashboards, or local sessions.

Do not use local planning mirrors as canonical sources.

## Process

1. Resolve the Doppler target from repo setup or known `DOPPLER_PROJECT` and `DOPPLER_CONFIG`. If unclear, stop and ask for the target.
2. Inventory every required secret, public config value, credential, and backing provider resource. Normalize names as uppercase Doppler env vars and dedupe by provider, environment, owner, scope, and rotation boundary.
3. Check Doppler by name only: `command -v doppler`, `doppler --version`, and `doppler secrets --only-names`. Never read or print secret values.
4. Inspect authenticated provider accounts before asking the human. Safe discovery may list non-secret metadata such as resource names, IDs, regions, plans, domains, enabled products, and project names.
5. Reuse existing provider resources when they fit the project without weakening isolation, permissions, ownership, environment boundaries, or billing expectations.
6. For missing or ambiguous resources, present a short reuse/create/human plan with a recommendation. Ask the user to verify the plan before creating resources, rotating credentials, enabling products, changing billing, broadening permissions, or choosing among ambiguous accounts.
7. After verification, create provider resources with official tooling when appropriate, then pipe generated or recoverable values directly into Doppler without printing or saving them.
8. Generate app-owned values locally only when the app owns the secret, such as session, signing, CSRF, encryption, webhook development, or test-only random values.
9. For genuinely human-required values, give short setup steps that put the value directly from the user's clipboard into Doppler; do not ask the user to reveal the value.
10. Finish with name-only verification and report present, recovered, created, pending verification, and human-required names.

## Classification

Classify each missing value with the first safe match:

- `present`: already exists in Doppler by name.
- `recoverable`: authenticated official tooling can retrieve the exact value or required public config and pipe it into Doppler without exposure.
- `verified-create`: the user verified a provider resource plan, official tooling creates it, and generated values can be sent directly to Doppler.
- `generate-local`: Codex can create an app-owned random value and pipe it to Doppler.
- `current-env`: the exact value is already in the current process environment and can be piped to Doppler.
- `human-required`: the value must be created, viewed, copied, approved with MFA, billed, guessed, disambiguated, or retrieved by a command that would expose or persist it.

Human-required usually includes provider API keys, OAuth client secrets, database passwords, cloud private keys, service account JSON, webhook signing secrets from real dashboards, billing-gated keys, account-owned tokens, and one-time dashboard secrets.

## Safe Commands

Use Doppler only:

```sh
command -v doppler
doppler --version
doppler secrets --only-names
```

Use non-printing writes only:

```sh
provider-cli get-secret --name SECRET_NAME --project "$PROVIDER_PROJECT" 2>/dev/null \
  | doppler secrets set SECRET_NAME --silent
```

```sh
printenv SECRET_NAME \
  | doppler secrets set SECRET_NAME --silent
```

```sh
openssl rand -base64 48 \
  | doppler secrets set SECRET_NAME --silent
```

Do not run commands that print secret values, dump broad environments, write credential files, place real secrets in shell arguments, or require Codex to copy values from a dashboard.

## Human Setup Output

For each human-required secret, provide one concise step:

````md
### SECRET_NAME

Get it: {official provider or dashboard link}
Copy: {exact provider UI label, such as API key or Client secret}
Used by: {issues/features/slices}
Notes: {scope, environment, owner, expiration, rotation, or permission note}

```sh
pbpaste | doppler secrets set SECRET_NAME --silent
printf '' | pbcopy
```
````

Use explicit Doppler scope only when required:

```sh
pbpaste | doppler secrets set SECRET_NAME -p "$DOPPLER_PROJECT" -c "$DOPPLER_CONFIG" --silent
printf '' | pbcopy
```

Then verify names only:

```sh
doppler secrets --only-names
```

## Rules

- Do not write secret files, `.env` files, inventories, logs, or local mirrors.
- Do not include actual secret values in chat, code, commands, Linear, files, summaries, or commits.
- Do not ask the user to paste secret values into Codex.
- Do not read Doppler secret values; use name-only checks.
- Do not use `doppler secrets set SECRET=value` for real secrets.
- Do not invent provider scopes, permissions, credential types, regions, or product plans.
- Use official provider docs or dashboards when setup steps are not obvious.
- List every issue, slice, or feature that consumes a reused secret under `Used by`.
- Stop when the required value is unsafe to recover automatically, the provider account is ambiguous, or the Doppler target is unclear.
