---
label: FAQ
icon: question
---

# Frequently Asked Questions

:::info
Common questions about Drew's security model, permissions, control, recovery, and behavior.
:::

## Control

### What happens if the server owner account is compromised?

Drew's control should not depend entirely on a single Discord account.

Configure your recovery options before deploying Drew and keep your recovery credentials stored securely and outside of Discord.

:::warning
Treat recovery credentials as highly sensitive. Anyone with access to them may be able to regain control of Drew.
:::

### Who can manage Drew?

Drew separates Discord ownership from operational access.

Access should only be granted to users who require it, with the minimum level of control necessary for their role.

:::warning
Do not grant elevated Drew access simply because a user is a server administrator. Administrative access to Drew can bypass protections that apply to normal members.
:::

### Can an administrator bypass Drew's protections?

Depending on the protection being triggered, Discord permissions and Drew's internal authorization system are separate layers.

A user having `Administrator` in Discord does not automatically mean they should have unrestricted access to Drew's control plane.

---

## Security Model

### How does Drew determine whether an account or action is suspicious?

Drew does not rely on a single signal.

Security decisions can take multiple factors into account, including account characteristics, server context, configured thresholds, and the type and frequency of actions being performed.

A suspicious signal does not necessarily mean an account is malicious. It contributes to Drew's overall decision-making.

### Which Discord permissions are considered dangerous?

The most security-sensitive permissions include:

- `Administrator`
- `Manage Server`
- `Manage Channels`
- `Manage Roles`
- `Manage Webhooks`
- `Manage Messages`
- `Kick Members`
- `Ban Members`
- `Moderate Members`

These permissions can allow an account or integration to make destructive or high-impact changes to a server.

### How can I determine whether my server is properly protected?

Use Drew's dashboard to review the current security state of the server.

Pay particular attention to:

- Role hierarchy
- Dangerous permissions
- Whitelists
- Protected integrations
- Channel access
- Security module configuration
- Recovery configuration

A secure configuration is not a static state. Review it whenever roles, bots, integrations, or permissions change.

---

## Enforcement

### Why didn't Drew punish a user?

If Drew detected an action but did not enforce a punishment, check the following:

- The relevant module is enabled.
- The configured threshold was reached.
- The user or their role is not whitelisted.
- The user does not have an exemption or elevated Drew permission.
- Drew's role can act on the target.
- The configured punishment role can actually be applied.
- No Discord permission or hierarchy restriction prevented the action.

If the behavior is still unexpected, reproduce it and collect the relevant event details before changing multiple settings at once.

### Why is Drew punishing a legitimate integration?

Security systems cannot inherently distinguish every legitimate automation from malicious behavior.

An integration performing high-volume or high-impact actions may trigger the same protections designed to stop abuse.

If the integration is trusted, explicitly scope the required exemption instead of disabling the entire protection module.

:::warning
Prefer narrowly scoped whitelists over globally disabling security protections.
:::

### Why is Drew blocking or quarantining my automation?

Bots that modify channels, roles, webhooks, messages, or members can trigger security controls when their behavior matches a protected action pattern.

Review the event that triggered the enforcement and determine whether the integration actually requires the affected permission.

Only exempt the integration from the specific protection it legitimately requires.

### Why are my webhooks being removed or blocked?

Webhook activity can trigger enforcement when it matches configured security thresholds or patterns.

Before whitelisting the webhook, verify:

- Which integration created it.
- Which actions it performed.
- Whether the behavior is expected.
- Whether the integration was recently modified or compromised.

Do not whitelist a webhook simply because its owner is trusted.

---

## Response & Diagnostics

### Why is Drew not responding to commands?

Check the failure in this order:

1. Verify Drew is online.
2. Confirm Drew can access the channel.
3. Verify `Send Messages` and `Read Message History`.
4. Confirm the command is available in the current context.
5. Check the configured command prefix or invocation method.
6. Verify that the user is not restricted by Drew.
7. Check Drew's service status.

If the issue persists, use the troubleshooting workflow before changing the server configuration.

### Why does Drew sometimes take longer to respond?

Command latency can be caused by Discord API latency, service-side processing, or temporary infrastructure issues.

A short delay is not necessarily a failure.

If commands consistently take several seconds to respond, collect timestamps and relevant command information and report the issue.

### Drew is online, but nothing is being enforced. Why?

Being online does not necessarily mean that every security module is operational.

Check:

- Module state
- Required permissions
- Role hierarchy
- Configuration
- Whitelists and exemptions
- Thresholds
- Target eligibility

A protection that appears inactive should be diagnosed from its configuration and event state rather than by repeatedly triggering it.

---

## Configuration

### Why does Drew say it is missing permissions?

Drew requires specific Discord permissions for different operations.

If a required permission is missing, restore the permission and verify the effective permissions on the affected channel or category.

Also check the role hierarchy. Having the permission alone is insufficient if Discord prevents Drew from acting on the target.

### Why does Drew work in one channel but not another?

Discord permissions are evaluated per channel and can be overridden by category or channel-specific permissions.

Compare the effective permissions in both locations rather than only checking Drew's role configuration.

### Why can't Drew moderate a specific member?

The most common cause is Discord's role hierarchy.

Drew cannot moderate members whose highest role is equal to or higher than Drew's highest role.

Check the target's highest role, Drew's highest role, and any relevant role-management restrictions.

---

## Recovery

### What should I do before giving Drew control of a production server?

Before enabling security enforcement, verify:

- Drew's permissions.
- Drew's role position.
- Recovery configuration.
- Trusted administrators.
- Whitelists.
- Protected integrations.
- Security thresholds.
- Logging and diagnostics.

Run controlled tests before relying on Drew for production protection.

### What happens if I accidentally lock myself out?

Do not immediately remove Drew or disable its security modules.

First use the configured recovery mechanism or an authorized account with sufficient Drew access.

If neither is available, contact support with the server and diagnostic information required to verify ownership.

:::warning
Never share recovery credentials, authentication tokens, or sensitive configuration data publicly.
:::

---

## Trust & Abuse

### I found another bot claiming to be Drew. Is it legitimate?

Be cautious with unsolicited bots, DMs, QR codes, authentication requests, and verification links claiming to be Drew.

Never scan an authentication QR code or authorize an unknown application simply because it claims to be Drew.

Verify the bot's identity through Drew's official documentation and support channels.

:::danger
Drew will never require you to hand over your Discord account credentials or scan an unexpected authentication QR code to "verify" your server.
:::

### What should I do if I encounter a fake Drew?

Do not interact with it further.

Remove it from the server if you have sufficient permissions, revoke any suspicious authorizations, and report the account or application to Discord.

If you believe the impersonation is related to Drew, report it through the official [Drew support channel](https://discord.gg/stane) with the relevant evidence.
