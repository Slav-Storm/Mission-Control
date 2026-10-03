# Codex inbox authentication — investigation and implementation report

Updated 2026-10-03. Automatic/recurring invocation remains disabled. The inbox can still provide its bounded manual handoff. This change does not enable scheduling, replace a credential, approve a new binary, or grant robot authority.

## Supported path

The installed Codex CLI is `0.158.0-alpha.2`. Its native `login status` and `exec` interfaces are present. Official [authentication documentation](https://learn.chatgpt.com/docs/auth) describes ChatGPT subscription login and the client-owned cached credential store. [Non-interactive documentation](https://learn.chatgpt.com/docs/non-interactive-mode) documents `codex exec` reusing saved authentication. ChatGPT and API-key billing are different paths; this adapter permits only the former.

`auth.mjs` asks the hash-pinned client to run `login status` using its supported automatic credential-store selection. It never opens or copies a credential store, calls login/logout, extracts desktop tokens, or connects directly to an undocumented backend. Only a successful `Logged in using ChatGPT` result qualifies. Unknown formats fail closed.

The checker calls the existing single-writer service; it never handles Codex credentials. A nonempty eligible inbox, explicit enabled policy, migration proof and matching executable hash must all pass before native authentication preflight. The read-only operator then checks authentication again immediately before inference, protecting against a session disappearing after claim.

The subprocess environment excludes API keys, tokens, credential variables and API endpoint overrides without reading excluded values. Client-owned auth discovery and host sandbox restrictions remain available. Exec skips user configuration and explicitly sets `forced_login_method="chatgpt"`, the built-in OpenAI provider and automatic credential-store selection. No direct API request or separately billed fallback exists. ChatGPT session refresh remains the client's responsibility.

## Current observed limitation

Both default-store and automatic-store `login status` returned signed out **in this execution context**. That does not mean the desktop app itself is signed out. No supported reusable saved ChatGPT session is currently available to this checker context. The development configuration has no invocation binding and the service policy is disabled. Windows task inspection returned PermissionDenied, so this investigation does not claim fresh OS-level task verification. It did not enable any task.

The reported HTTP 401 was not reproduced using an inference call. No model was invoked. A mock 401 confirms failure handling only. The older isolated CLI proof remains historical evidence; its removed executable does not approve the newly installed binary or authenticate this context. Do not silently rebind it.

For now use the existing `check-inbox --dry-run` or normal disabled-policy manual handoff through the PC service. A future supported-session test would need a native ChatGPT login available in the same OS user context, a separately verified current binary binding and the existing migration gates. This task does not authorize recurring activation. Do not copy a desktop session, supply a service credential, use `--with-api-key`, or purchase API usage to make the test pass.

## Durability and privacy

- Empty and human-only inboxes start no model and no auth probe. Disabled policy and dry runs do not probe auth.
- Failed preflight leaves tickets open and unclaimed, starts zero models and disables automatic policy. Manual handling and deduplication remain intact.
- A session disappearing after claim but before exec records `NOT_STARTED`, reopens the ticket, spends no daily model allowance and disables retries.
- A launched process returning 401 records a failed invocation, holds the ticket for review and disables automatic policy. It is not silently repeated.
- Async preflight rechecks policy and queue ownership before claim. Human pauses and another active invocation win.
- CLI stdout/stderr exist only in bounded process memory. Raw error/event/final-output streams are never written to artifacts. Credential-like briefs and results are rejected. Only schema-validated proposals, fixed diagnostic codes and numeric usage counts are persisted. No `--output-last-message` file is used.
- The client still owns its normal credential store and any client-internal diagnostics. Mission Control does not read or copy them. No promise is made that regex detection can identify arbitrary unknown secrets; the primary protections are no secret input, no raw output persistence, native auth and no tools.

## Evidence and limits

Local verification evidence contains only classified native status and safe configuration booleans. A local checkpoint preserves the prior implementation. Runtime data, credentials, machine paths and raw evidence are not included in this documentation repository. New simulated tests cover auth classification, forbidden environment variables, timeout/output bounds, session loss, 401 redaction, policy pauses, manual fallback and existing dedup/budgets/human gates.

The full PC Node suite passed 225 tests and viewer suite passed 25. The existing telemetry-recovery Python suite passed. The 23 PC and 21 legacy Lua-dependent suites could not import `lupa.LuaRuntime`, so their checks did not execute. This is not physical Minecraft evidence, a successful authenticated inference, or completed migration acceptance.

## Verification summary

| Check | Result | Evidence type |
| --- | --- | --- |
| Installed CLI version | 0.158.0-alpha.2 | Native executable inspection |
| Saved session, default store | Signed out in this execution context | Native login status; no inference |
| Saved session, automatic store | Signed out in this execution context | Native login status; no inference |
| Service recurring invocation policy | Disabled | Read-only configuration/ledger inspection |
| Current invocation binding | Absent | Read-only configuration inspection |
| Windows scheduled-task status | Inspection denied | No fresh OS-level confirmation |
| Focused authentication/inbox tests | 29 passed, including final hardening changes | Simulated processes and isolated ledgers |
| Complete PC Node suite | 225 passed | Isolated regression tests |
| Viewer suite | 25 passed | Isolated regression tests |
| Telemetry recovery | Passed | Existing Python regression |
| PC Lua-dependent suites | 23 blocked before execution | Existing runtime import failure |
| Legacy Lua-dependent suites | 21 blocked before execution | Existing runtime import failure |
| Real model calls during this investigation | Zero | No inference attempted |
| Development-colony actions during this investigation | Zero | No physical dispatch or deployment |

The 29 focused tests are included in the 225 PC tests, not additional to them.
The full PC suite preceded the final stricter auth-status/null-result checks; the
focused 29 were rerun afterward and all passed. The Lua import failures do not
count as passed runtime or physical tests.

## Outcome and next gate

**Implementation complete for the authentication safeguards; automatic invocation
not verified or enabled.** The installed client exposes a documented ChatGPT
session path, but that session is unavailable in the inspected execution context.
The current outcome is manual inbox handoff. This does not establish that
subscription-backed unattended execution is universally unsupported.

Before a future bounded live invocation test, the native client must independently
report an available ChatGPT login in the same user context and the current binary
must satisfy its own proof binding. Existing migration and human gates still apply.
Do not enable recurring invocation merely because authentication later succeeds.
No API-key workaround, credential extraction or separately billed provider is
part of this implementation.

The wider PC Mission Control migration remains incomplete. This authentication
checkpoint does not change quest reservations, grant standing operations, or
claim completion of any outstanding physical ministry acceptance test.
