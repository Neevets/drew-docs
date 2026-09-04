---
label: Permissions
icon: checklist
---

# Permissions

Drew requires elevated Discord permissions to reliably perform security, moderation, and Auto-Rollback actions.

Discord permissions are evaluated together with channel overrides and role hierarchy. Granting a permission on Drew's role does not necessarily mean that Drew can use it in every channel or against every target.

:::danger Administrator Required
Drew requires the `Administrator` permission for its security and moderation functionality.

Removing `Administrator` can cause individual modules or enforcement actions to fail even if Drew remains online and responsive.
:::

## Administrator

`Administrator` grants Drew unrestricted access to Discord permissions and is required for Drew's full protection model.

This allows Drew to operate across the server without requiring individual permission configuration for every security action.

:::warning
`Administrator` does not override Discord's role hierarchy. Drew still cannot manage roles or members positioned at or above its highest role.
:::

## Role Hierarchy

Drew's role must be positioned high enough to perform the actions required by its enabled modules.

The hierarchy affects operations such as:

- Managing roles
- Moderating members
- Applying quarantine roles
- Performing enforcement actions
- Managing resources protected by Drew

Place Drew's role above the roles and members it needs to manage.

## Channel Permissions

Even with `Administrator`, channel-specific configuration can affect Drew's ability to operate in restricted contexts.

For command and message-based functionality, verify:

- `View Channel`
- `Send Messages`
- `Read Message History`

Check both the affected channel and its parent category for explicit permission overrides.

## Permission Failures

If Drew reports missing permissions or an action fails unexpectedly:

1. Check Drew's effective permissions in the affected channel.
2. Check category and channel overrides.
3. Verify Drew's role position.
4. Confirm the required permission is available for the specific operation.
5. Retest the operation after making a single change.

Do not remove security protections to compensate for a permission problem. Identify and correct the underlying permission or hierarchy issue instead.

## Recommended Configuration

For the most reliable deployment:

- Keep `Administrator` enabled for Drew.
- Position Drew's role above the roles it must manage.
- Avoid unnecessary channel-specific denies.
- Review permission overrides after modifying categories or protected channels.
- Revalidate Drew's effective permissions whenever the server's role structure changes.

For installation, continue with [Installation](installation.md).

If Drew has the expected permissions but still cannot perform an action, see [Troubleshooting Guide](../guides/troubleshooting.md).
