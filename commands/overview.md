---
label: Overview
icon: wrap
order: 9
---

# Overview

Drew provides a command interface for managing security systems, moderation, configuration, diagnostics, and server utilities.

Commands are organized by function so you can quickly locate the system you need.

:::info Command Usage
Commands may require specific permissions, modules, or configuration before they can be used successfully. If a command does not respond or returns a permission error, check the [Troubleshooting Guide](../guides/troubleshooting.md).
:::

## Permissions

Command access is determined by Drew's permission model and, where applicable, Discord permissions.

Some commands can perform high-impact operations. Treat administrative and security commands as privileged operations and only grant access to trusted staff.

:::warning
Discord `Administrator` permission does not automatically grant unrestricted access to every Drew command. Drew may apply its own authorization rules to sensitive operations.
:::

## Command Behavior

Before executing a command that changes server state, verify:

- You understand what the command will modify.
- You have the required Drew permissions.
- Drew has the Discord permissions required for the operation.
- The affected resources are correctly configured.
- The command is being executed in the intended server and channel.

For security-sensitive operations, prefer controlled testing before applying changes to production resources.

## Troubleshooting Commands

If Drew is not responding or a command behaves unexpectedly, first verify:

- Drew is online.
- The command is enabled and supported.
- The current channel is accessible to Drew.
- Required permissions are available.
- The relevant module has been configured.
- The command is being executed in a supported context.

For a complete diagnostic workflow, see [Troubleshooting](../setup_guide/troubleshooting.md).
