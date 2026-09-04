---
label: Troubleshooting
icon: thumbsup
---

# Troubleshooting

Use this runbook to diagnose cases where Drew is unresponsive, unable to perform an action, or behaving differently from its configured state.

:::danger Incident Handling
Do not modify multiple configuration variables at once. Apply one change, retest, and record the result before making another change. This preserves the original state and makes the root cause easier to identify.
:::

## 1. Establish the Failure

Before changing anything, identify exactly what is failing.

Record:

- The affected server
- The affected channel or resource
- The exact command, action, or module involved
- Whether the issue affects one user or multiple users
- Whether the issue is reproducible
- The approximate occurrence time in UTC

Classify the failure:

- **No response:** Drew does not acknowledge the command or event.
- **Permission failure:** Drew responds but cannot perform the requested action.
- **Configuration failure:** Drew behaves differently from its configured state.
- **Enforcement failure:** A configured security action is not triggered.
- **Platform failure:** Discord, Drew, or a required external dependency is unavailable.

Correctly classifying the failure helps determine where to investigate.

## 2. Verify Drew's Runtime State

Confirm that:

- Drew is present in the server.
- Drew is online.
- The affected command or module is enabled.
- The current configuration has been applied successfully.
- The issue is not limited to a specific command or module.

If Drew is unavailable across the server, check Drew's service status and Discord's status before modifying the server configuration.

## 3. Verify Effective Discord Permissions

Do not rely solely on the permissions displayed on Drew's role. Discord permissions can be affected by role configuration, category overrides, channel overrides, and explicit denies.

In the affected channel, verify the permissions required by the failing operation.

For command and message-based functionality, check:

- `View Channel`
- `Send Messages`
- `Read Message History`

For moderation and security operations, verify every permission required by the specific action.

:::warning
A permission enabled on Drew's role does not guarantee that Drew has that permission in the affected channel.
:::

Check both the affected channel and its parent category. Pay particular attention to explicit deny overrides.

## 4. Verify Role Hierarchy

If Drew detects an event but cannot act on the target, inspect the server's role hierarchy.

Confirm that:

- Drew's highest role is above the target member's highest role.
- Drew's role is above every role it needs to manage.
- No managed or integration role prevents the required action.
- The target is not otherwise protected by Discord's hierarchy rules.

:::warning
`Administrator` does not bypass Discord's role hierarchy. Drew cannot moderate members or manage roles positioned at or above its highest role.
:::

## 5. Verify Command Context

If the issue affects a command, verify:

- The command is valid.
- The command is enabled.
- The current channel supports the command.
- The user is authorized to invoke it.
- Drew can access and respond in the current channel.
- Any required module or initialization step has been completed.

If the same command works in one channel but not another, investigate channel permissions and context before changing Drew's global configuration.

## 6. Check Module Configuration

If only one security or utility module is affected, inspect that module before changing global Drew settings.

Verify:

- The module is enabled.
- Its configuration is valid.
- Required thresholds are configured correctly.
- The actor or resource is not whitelisted.
- The actor does not have an exemption or elevated Drew permission.
- Required protected resources are configured correctly.

For enforcement issues, verify the complete process:

**Event detection, eligibility checks, threshold evaluation, enforcement, and Discord permission validation.**

A failure at any stage can prevent the expected action from occurring.

## 7. Investigate Enforcement Failures

If Drew detects an action but does not punish, quarantine, block, or otherwise enforce against it, check:

1. Was the event detected?
2. Did the event meet the configured threshold?
3. Was the actor eligible for enforcement?
4. Was the actor or affected resource whitelisted?
5. Did Drew have the permissions required for the action?
6. Was the target below Drew in the role hierarchy?
7. Was the relevant protection enabled when the event occurred?

Do not disable a protection because of an unexpected result. Identify which part of the enforcement process prevented the action first.

## 8. Investigate Auto-Rollback Failures

If Drew detected a destructive action but did not restore the affected resource, verify:

- Auto-Rollback is enabled for the relevant protection.
- The event type supports rollback.
- Drew had sufficient permissions to restore the resource.
- The previous resource state was available for restoration.
- The action was not excluded by a whitelist or configuration rule.
- Discord accepted the restoration request.

Detection and rollback are separate operations. Drew may successfully detect a destructive action while being unable to restore the affected resource.

## 9. Investigate Integrations

If the issue only occurs with another bot, webhook, or external integration:

- Identify the integration performing the action.
- Determine exactly what actions it is performing.
- Confirm whether Drew is detecting those actions as potentially destructive.
- Review the relevant whitelist or exemption.
- Prefer a narrowly scoped exemption over disabling the protection globally.

:::warning
Do not whitelist an integration solely because it is trusted. Verify which actions and permissions it actually requires.
:::

## 10. Check External Dependencies

Only investigate external dependencies when the affected feature actually depends on them.

Depending on the module, verify the availability and configuration of:

- Antivirus or AV services used by security-related functionality
- Sentry for error reporting
- Better Stack for observability
- Redis for state or caching operations
- Database services for persistent configuration or state

Do not assume an external dependency is responsible until the failure has been isolated to a feature that uses it.

## 11. Check Platform and Service Health

If Drew is correctly configured but commands or events are intermittently delayed or unavailable:

- Check Discord's service status.
- Check Drew's service status.
- Compare the behavior across multiple channels where possible.
- Record the exact UTC timestamps of failures.

Avoid repeatedly changing permissions during a suspected platform outage. Preserve the existing configuration and retest after service health has recovered.

## 12. Collect Diagnostics

If the issue remains reproducible, collect the following information:

- Server ID
- Channel ID
- User or target ID, when relevant
- Exact command or action
- Exact error message
- Approximate UTC timestamp
- Affected module
- Expected behavior
- Actual behavior
- Relevant screenshot or copied output

:::danger
Never include tokens, passwords, recovery credentials, private keys, or other authentication secrets in diagnostic reports.
:::

## Fast Isolation

If Drew is online but appears completely unresponsive:

1. Test the same operation in a controlled private channel.
2. Verify `View Channel`, `Send Messages`, and `Read Message History`.
3. Check channel and category overrides.
4. Verify Drew's role position.
5. Confirm the affected command or module is enabled.
6. Check Drew and Discord service status.

If the operation works in the controlled channel, investigate channel permissions, overrides, and command context first.

## Failure Isolation Matrix

| Symptom | First layer to inspect |
| --- | --- |
| Drew is offline | Drew or Discord service |
| No command response | Channel permissions or command context |
| Works in one channel only | Channel or category overrides |
| Command responds but action fails | Operation permissions |
| Cannot moderate a member | Role hierarchy |
| Security event detected but not punished | Module configuration or eligibility |
| Legitimate bot gets punished | Integration configuration or whitelist |
| Action detected but not restored | Auto-Rollback, permissions, or resource state |
| Only one module fails | Module configuration or dependency |
| Multiple modules fail simultaneously | Drew, Discord, or infrastructure |

## Escalation

If the issue persists after completing the relevant checks:

1. Preserve the current configuration.
2. Record the exact reproduction steps.
3. Capture all relevant IDs and UTC timestamps.
4. Document the expected and actual behavior.
5. Include the exact error output.
6. Escalate with the collected diagnostics.

Do not perform destructive tests on a production server solely to reproduce an issue unless the impact is understood and the test has been explicitly authorized.
