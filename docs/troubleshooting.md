# Troubleshooting

[Back to README](../README.md)

Start with the section matching the symptom. Keep an existing task ID when investigating a generation or processing problem so your agent can check that task instead of creating another one.

## Connection and sign-in

### The agent cannot connect

1. Compare the configured URL and transport with the [connection settings](../README.md#quick-start). Include the `/mcp` path.
2. Check that your agent version supports the options in the setup command. An unrecognized option is an agent setup issue; update the agent using its official installation instructions.
3. Inspect the server in the agent's MCP settings (`/mcp` in Codex or Claude Code). If it is absent, follow the relevant [quick start](../README.md#quick-start).
4. If it is present but unreachable, check whether your network, proxy, VPN, or organization policy blocks the service or OAuth sign-in. Follow your organization's access process where applicable.

If the connection still fails, [report the issue](#reporting-an-issue) with the agent version and exact error text.

### Browser authorization fails or the session expires

Start authentication again using your agent's [sign-in steps](../README.md#quick-start). Sign in to the intended Fotor account and complete the browser flow before returning to the agent. If the terminal provides an authorization URL instead of opening a browser, open that URL yourself.

Check the agent for any callback or authorization error. If authorization repeatedly fails, report the error message and the step at which it fails. Share a sanitized error rather than the authorization URL or code.

### A signed-in Fotor website link has expired

Ask your agent for a fresh Fotor website link and open it yourself. These links are one-time links; automated previews can consume them.

## Tools not appearing

1. Open your agent's MCP settings (`/mcp` in Codex or Claude Code) and check that the Fotor connection is active and authenticated.
2. Check whether the agent has disabled the server or restricted its tools. Enable the tools you intend to use where your permissions allow it.
3. After changing the connection, start a new agent session to reload its tools.
4. Ask explicitly: “Use Fotor to list the available image models.”

If only some tools appear, service-side availability may be the cause. Report which tools are visible and which capability you expected if reconnecting does not resolve it.

## Credits and plans

### A task reports insufficient credits

Ask your agent to check your balance. If the error includes a plans link, open it to review the available Fotor plans. This page describes plans; it is not a per-task MCP price list.

After resolving the balance issue, ask your agent to submit the task again when you are ready. Account, payment, and order questions belong in the [Fotor Help Center](https://support.fotor.com/hc/en-us).

### The balance is unavailable

`credits_unavailable` means balance information could not be retrieved for the account. It does not mean the balance is zero, and it is not necessarily an authentication failure.

Confirm that you authorized the intended Fotor account. A successful model-list request can help distinguish a working MCP connection from a balance-specific problem. If the error continues, contact support with the error code. For `not_configured`, report a service configuration issue; local configuration changes cannot supply the missing service setting.

### The plans page asks me to sign in

A plans link does not establish a browser session. Sign in on the website, or ask your agent for a signed-in Fotor website link, open it yourself, and then visit the plans page in the same browser.

### A task reports credits that differ from my balance

The task field `credits_increment` reports that task's consumption, not your remaining balance. Use `get_credits` to request a balance. A null consumption value means it was not returned; it does not indicate a free task.

## Task status and results

### My task is still processing

Ask your agent to check the existing task ID again after a wait. Each `get_task` call checks once. The service does not provide a progress percentage or guaranteed completion time through this field.

A `processing` response can represent a queued, running, or temporarily unavailable task. Confirm the task ID and that you are using the Fotor account that submitted it. If repeated checks remain unresolved, report the task privately to support; repeated submissions can create separate chargeable tasks.

### Submission outcome is uncertain

`submission_uncertain` means the request may have reached the service and created a chargeable task even though confirmation was not received. **Do not automatically repeat the submission.**

If you have a task ID, check it. If no ID was returned, retain the approximate submission time, operation, and error message and contact support. A new submission should be an explicit decision after considering that the original may already exist.

### A status check fails

For `upstream_unavailable`, check the same task again later. Retrying a status check is different from resubmitting the creation request. For `invalid_parameters`, confirm that the task ID exactly matches the one returned by submission.

### The task failed or has no usable result

Report the returned `status` and `error`. A terminal `failed`, `timed_out`, or `cancelled` task has finished without a successful output. A nonterminal `unknown` status can be checked again later.

Even when a task reports completion, inspect `error` and `result_url`: moderation-blocked results have no output link. Do not present a missing result as a completed deliverable. If a previously returned link stops working, check the original task again; result links are not guaranteed to be permanent. Contact support if the output remains unavailable.

## Reference media and model settings

### My uploaded image, video, or audio cannot be used

Ask your agent to confirm that the file was uploaded successfully. Receiving an upload link alone does not upload the file. If the link expired before the upload finished, ask for a fresh link and upload again.

For an existing media URL, use an accessible HTTPS link to the media itself. A local path, a webpage containing the media, or a URL requiring a private browser session is not a usable reference. Check that the chosen model supports the reference type and format. If the tool reports “Media uploads are not configured,” report the service issue.

### A model rejects my settings

Ask your agent to inspect the chosen model with `list_models` and compare its supported mode, resolution, ratio, duration, quality, and reference types with the request. Use a currently listed model if the previous one has been retired.

First-frame and first/last-frame video need an explicit supported aspect ratio. Multimodal video also needs one when it has image references without video references. Generated audio must be supported by the model; adding an audio reference does not turn generated audio on.

## Reporting an issue

Use [GitHub Issues](https://github.com/fotor-ai/fotor-mcp/issues) for MCP connection problems, tool errors, and feature requests. Include:

- Agent name and version, operating system, and approximate time with time zone.
- The step or tool that failed and the exact sanitized error message.
- Expected behavior and what happened instead.
- Whether the problem repeats, and a minimal description of the input if relevant.

Keep tokens, cookies, authorization codes, signed upload URLs, one-time website links, and private media out of public issues. Provide account-specific details or task identifiers through official support when needed.

Use the [Fotor Help Center](https://support.fotor.com/hc/en-us) for account, payment, order, or private task investigations.
