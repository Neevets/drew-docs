---
label: Setup
icon: gear
---

# Setup

Drew's setup process configures the permissions, security modules, protection policies, and server resources required for reliable operation.

:::info
Complete the initial setup before enabling Drew's security features in a production environment.
:::

## Before You Start

Ensure that:

- Drew is installed and has the required permissions.
- Drew's role is positioned correctly in the server hierarchy.
- A private channel is available for configuration and testing.
- You have `Administrator` permission in the server.
- Any existing security or moderation integrations that interact with Drew have been identified.

## Initialize Drew

Start the setup process using Drew's setup command.

The setup process validates Drew's environment and configures the resources required by its security systems.

If Drew reports missing permissions, resolve the reported Discord permission or role hierarchy issue before continuing.

## Validate the Setup

After setup completes, verify that:

- Drew can access the required channels.
- Drew can perform the actions required by its enabled modules.
- Drew's role is above the roles it needs to manage.
- Security modules are enabled and configured as intended.
- Trusted users, bots, and integrations have been reviewed.
- Auto-Rollback is configured where required.

:::success
Do not consider setup complete solely because the setup command succeeds. Validate Drew's effective permissions and security behavior before relying on it in production.
:::

## Production Readiness

Before enabling Drew across a production server, review:

- Role hierarchy
- Effective channel permissions
- Security module configuration
- Thresholds
- Whitelists and exemptions
- Protected integrations
- Auto-Rollback configuration
- Diagnostic and logging configuration

Make configuration changes incrementally and validate the resulting behavior after each change.

## Troubleshooting

If setup fails or Drew reports that it lacks required permissions, see the [Troubleshooting Guide](../guides/troubleshooting.md).

If you have not installed Drew yet, start with [Installation](../getting_started/installation.md).
