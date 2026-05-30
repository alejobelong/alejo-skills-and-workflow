---
name: alejo-secrets
description: Use when a user wants required API keys, credentials, tokens, provider resources, provider config, or environment variables set up in Doppler for Alejo PRD/SAD slices, Linear issues, implementations, or Alejo Run. Automatically find existing authenticated provider resources, propose reuse-or-create plans for missing resources, recover safe values into Doppler, and only give human setup steps when truly required. Never write secret artifact files.
---

# Alejo Secrets

Set up required runtime secrets in Doppler. Prefer finding existing authenticated provider resources, creating missing resources after plan verification, and safely piping values into Doppler. Ask the human only when Codex truly cannot obtain or create what is needed safely.

Never ask the user to paste secret values into Codex, chat, files, logs, or code. Never write `.env`, secret inventories, or other secret artifact files.

## Process

### 1. Gather Inputs

Inspect the current request, Alejo XML docs, Linear issues/comments, `CONTEXT.xml`, ADRs, code, deployment config, CI, and env examples. If issue refs are provided, fetch them.

Identify every required secret, config value, and backing provider resource, including provider API keys, OAuth credentials, database URLs, webhook signing secrets, signing/encryption keys, service accounts, cloud resources, deploy tokens, observability sinks, and public provider config required at runtime.

Normalize names to Doppler-style env vars: uppercase letters, numbers, underscores, and not starting with a number. Deduplicate by normalized name, provider credential, environment, owner, scope, and rotation boundary. Reused secrets get one Doppler entry and a complete `Used by` list.

### 2. Use Doppler Only

Always use Doppler. Prefer the repo's configured Doppler scope from `doppler setup`; use explicit `-p "$DOPPLER_PROJECT" -c "$DOPPLER_CONFIG"` only when the project/config is known.

Safe Doppler checks:

```sh
command -v doppler
doppler --version
doppler secrets --only-names
```

Do not run commands that print secret values. Never include real secret values in chat output.

### 3. Discover Provider Resources

Before asking the human for a secret, inspect authenticated provider accounts with official CLIs, MCP connectors, APIs, or local auth sessions. Look for existing resources that satisfy the needed environment, project, region, plan, scopes, and product constraints.

Safe discovery may list non-secret metadata such as resource names, IDs, regions, plans, domains, project names, and enabled products. Do not print secret values, tokens, private keys, connection strings, passwords, or broad env dumps.

If a usable resource exists, prefer reuse when it fits the project and does not weaken isolation, ownership, permissions, or environment boundaries.

If no usable resource exists, prepare a short plan before any provider-side creation:

```md
I looked in {provider/account/project} and did not find a usable {resource}.

Recommendation: {reuse existing resource | create new resource}

Options:
1. Use existing {resource name/id}: {tradeoff}
2. Create new {suggested name}: {region/plan/scopes/cost/permissions}
3. Human creates it manually: {when this is safer}

Please verify which option to use.
```

Ask for verification before creating resources, rotating credentials, enabling products, changing billing, broadening permissions, or choosing among ambiguous accounts/projects. Once verified, create the resource with official tooling, then recover any generated values directly into Doppler when possible.

### 4. Classify Each Missing Value

For every missing value, choose the first safe matching class:

1. **Already in Doppler**: name-only check confirms it exists. Report it as present; do not read it.
2. **Existing provider resource**: authenticated provider discovery finds a matching resource and the needed value can be retrieved safely. Pipe it into Doppler.
3. **Verified new provider resource**: the user verifies a create plan, official tooling creates the resource, and generated credentials/config can be piped directly into Doppler.
4. **Generate locally**: create app-owned random values such as signing keys, session secrets, encryption salts, test-only local passwords, or generated webhook development secrets when the app owns the secret and no provider dashboard is involved.
5. **Current environment**: if the exact env var is already present in the current process or `doppler run` environment, pipe it directly into Doppler without printing it.
6. **Authenticated provider recovery**: if an official CLI, MCP connector, API, or local auth session is already authenticated and can retrieve the exact value or non-secret public config for the exact project/environment, pipe it directly into Doppler without showing or saving it.
7. **Human-required**: if the credential must be created, viewed, copied from a dashboard, approved through MFA, billed, guessed, disambiguated, or retrieved by a command that would expose or persist it, give the user a short setup guide.

Human-required examples usually include provider API keys, OAuth client secrets, database passwords, cloud private keys, service account JSON, webhook signing secrets, billing-gated keys, account-owned tokens, and dashboard-only one-time secrets.

### 5. Automatic Recovery Rules

Automatic recovery is allowed only when all are true:

- Doppler CLI works and the target Doppler project/config is clear.
- The provider account, project, resource, environment, and credential name are unambiguous from repo config, docs, issue contract, verified plan, or authenticated provider metadata.
- The command uses official provider tooling or an authenticated provider API.
- The value is sent directly to `doppler secrets set ... --silent` through a pipe or stdin.
- The value is not printed, echoed, logged, written to a file, committed, summarized, or passed as a shell argument.
- Any provider-side creation, rotation, product enablement, billing change, permission change, or ambiguous reuse choice has a verified plan from the user first.

Use non-printing patterns:

```sh
provider-cli get-secret --name SECRET_NAME --project "$PROVIDER_PROJECT" 2>/dev/null \
  | doppler secrets set SECRET_NAME --silent
```

```sh
printenv SECRET_NAME \
  | doppler secrets set SECRET_NAME --silent
```

For generated app secrets:

```sh
openssl rand -base64 48 \
  | doppler secrets set SECRET_NAME --silent
```

If the provider command can only print a broad list, write a file, show a dashboard page, or expose the value in terminal output, do not run it. Move that secret to the human guide.

### 6. Research Human-Required Secrets

For each human-required secret, use official provider docs or dashboard/account URLs. Search online when the exact source or credential type is not obvious; prefer official sources. If subagents are available and delegation is allowed, a research subagent may look up provider URLs and setup steps, but must never receive secret values.

For ambiguous product decisions or credential scopes, ask a concise multiple-choice question with a recommended option. Do not invent provider scopes or credential types.

### 7. Output

Start with a short status:

- `Present in Doppler`: names only.
- `Recovered automatically`: names only and source type, never values.
- `Resource plan needs verification`: provider/resource options and recommendation.
- `Needs human setup`: names only.

Then provide one copy-pasteable step per human-required secret:

````md
### SECRET_NAME

Get it: {official provider link}
Copy: {exact provider UI label, such as "API key" or "Client secret"}
Used by: {slice/issue/feature names}
Notes: {scope, environment, owner, expiration, or rotation note}

```sh
pbpaste | doppler secrets set SECRET_NAME --silent
printf '' | pbcopy
```
````

When explicit Doppler scope is required:

```sh
pbpaste | doppler secrets set SECRET_NAME -p "$DOPPLER_PROJECT" -c "$DOPPLER_CONFIG" --silent
printf '' | pbcopy
```

Finish with name-only verification:

```sh
doppler secrets --only-names
```

Optionally include runtime verification when a project command is known:

```sh
doppler run -- sh -c 'test -n "$SECRET_NAME" && echo "SECRET_NAME is available"'
```

## Rules

- Do not write files.
- Do not create or update secret artifact files.
- Do not include actual secret values.
- Do not ask the user to paste secret values into Codex.
- Do not suggest 1Password or another secret manager.
- Do not use `doppler secrets set SECRET=value` for real secrets.
- Do not read Doppler secret values; use `doppler secrets --only-names`.
- Do not rely on memory for provider key locations; use official current docs or dashboards.
- Do inspect authenticated provider accounts for existing usable resources before asking the human for a secret.
- Do propose reuse-or-create options when a resource is missing or ambiguous.
- Do create provider resources only after the user verifies the plan.
- Do automatically recover values when they satisfy the automatic recovery rules.
- Do stop and ask only when the value is genuinely human-required or unsafe to retrieve automatically.
- Do include one command pair per unique human-required Doppler secret.
- Do list every slice, issue, or feature that consumes a reused secret under `Used by`.
- Do clear the clipboard immediately after every `pbpaste | doppler secrets set ... --silent` command.
