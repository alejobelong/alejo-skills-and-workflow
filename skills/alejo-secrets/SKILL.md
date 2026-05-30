---
name: alejo-secrets
description: Use when a user wants a Doppler-only, step-by-step terminal guide for creating required secrets, API keys, credentials, tokens, or environment variables for PRD/SAD vertical slices or implementation issues, or when Alejo Run needs safe recovery of missing Doppler secrets. Deduplicate reused secrets and research provider key sources online. Always use Doppler. Do not write secret artifact files.
---

# Alejo Secrets

Guide the user through creating required secrets in Doppler, secret by secret, with official provider links and copy-paste terminal commands. Never ask the user to paste secret values into Codex, chat, files, logs, or code.

Do not create or update secret artifact files. Output the guide in the conversation only.

## Process

### 1. Gather Context

Use the current context window, then inspect PRD XML, SAD XML, issues, latest Alejo Questions XML log, `CONTEXT.xml`, ADR XML docs, code, deployment config, CI, and env examples. If issue refs are provided, fetch bodies/comments.

### 2. Use Doppler

Always use Doppler. Do not ask the user to choose a provider.

Verify Doppler CLI access with safe commands only, such as `command -v doppler`, `doppler --version`, or `doppler secrets --only-names`. Do not run commands that print secret values.

Do not run `doppler secrets set` yourself unless one of these is true:

- The user explicitly asks and confirms the correct secret value is already on the clipboard.
- Alejo Run invoked this skill for safe automatic recovery of a missing generated application secret, current-process environment value, or verified non-secret public config value.

Safe automatic recovery must use non-printing commands only. Never print, log, paste, summarize, or echo secret values.

Prefer the repo's existing Doppler scope from `doppler setup`. If the project/config is known and should be explicit, use `-p "$DOPPLER_PROJECT" -c "$DOPPLER_CONFIG"`.

### 3. Inventory Secrets

Identify the required Doppler secret names for each slice or feature: API keys, external APIs, OAuth/client credentials, DB URLs, webhooks, signing/encryption keys, service accounts, cloud resources, CI/deploy tokens, and observability/audit sinks.

Normalize names to Doppler-compatible env vars: uppercase letters, numbers, and underscores; do not start with a number.

Deduplicate by normalized secret name, provider credential, environment/config, and required scope. If the same secret is needed by multiple slices, issues, or slides, ask for it once, create one Doppler entry, and list every consumer under "Used by". Create separate secrets only when scope, owner, environment, rotation policy, or credential type must differ.

### 4. Research Provider Key Sources

Use a research sub-agent for a deep online search when sub-agents are available and delegation is allowed in the current request. Give the sub-agent only the provider names, product names, required capabilities, and candidate secret names; do not give it secret values.

Ask the sub-agent to return:

- Provider/product name.
- Exact credential type needed, such as API key, personal access token, OAuth client secret, webhook signing secret, service account JSON, or cloud access key.
- Recommended Doppler secret name.
- Official provider URL where the user can create or view the credential.
- Short steps for what the user should click or copy.
- Notes about scopes, permissions, billing, expiration, or rotation that affect setup.

Require official provider docs or dashboard/account URLs when possible. Avoid blog posts unless official docs are unavailable. If the right credential type is ambiguous, surface a short open question instead of guessing.

### 5. Produce The Terminal Guide

Keep the guide short, complete, and copy-pasteable. Group by config only when needed.

Start with setup:

```sh
doppler login
doppler setup
```

If explicit project/config variables are needed:

```sh
export DOPPLER_PROJECT="{project}"
export DOPPLER_CONFIG="{config}"
```

Then list one step per unique secret. For each secret, include:

- What credential to create or copy.
- The official provider link.
- Any required scope/permission.
- Which slices, issues, or slides use it.
- The exact terminal command pair.

Use this shape:

````md
### SECRET_NAME

Get it: {official provider link}
Copy: {exact credential/value the provider UI labels, such as "API key" or "Client secret"}
Used by: {slice/issue/slide names or IDs that need this same Doppler secret}
Notes: {scope, environment, owner, expiration, or rotation note if relevant}

```sh
pbpaste | doppler secrets set SECRET_NAME --silent
printf '' | pbcopy
```
````

For command snippets, use:

```sh
pbpaste | doppler secrets set SECRET_NAME --silent
printf '' | pbcopy
```

When using explicit project/config variables:

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

## Output Rules

- Do not write files.
- Do not create a secret artifact file.
- Do not include actual secret values.
- Do not ask the user to paste secret values into Codex.
- Do not suggest 1Password or another provider.
- Do not use key-value `doppler secrets set SECRET=value` for real secrets.
- Do not rely on stale memory for where provider keys live; search online and prefer official provider sources.
- Do not provide generic "go to dashboard" guidance when an official URL or specific navigation path can be found.
- Do not automatically set provider API keys, OAuth client secrets, database passwords, cloud credentials, service account JSON, webhook signing secrets from a real provider dashboard, billing-gated keys, account-owned tokens, or any credential that must be guessed, retrieved from a private dashboard, read from files, or pasted into chat.
- Do allow Alejo Run to auto-set generated application secrets, exact-name current-process environment values, and verified non-secret public config values through non-printing Doppler commands.
- Do include one copy-paste command pair per secret.
- Do deduplicate reused secrets and include only one command pair per unique Doppler secret.
- Do list every slice, issue, or slide that consumes a reused secret under `Used by`.
- Do include the official provider link for each secret.
- Do include what exact provider UI value the user should copy.
- Do include `printf '' | pbcopy` immediately after every `pbpaste | doppler secrets set ... --silent` command.
- Do include open questions only when a required secret name, source, project, config, owner, or environment cannot be inferred.
