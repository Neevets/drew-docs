---
label: Installation
icon: mortar-board
---

# Installation

This guide covers the initial installation of Drew and the checks required to confirm that it is ready for configuration.

:::info Installation Requirements
You must have sufficient permissions to add applications to the target server. Drew requires the `Administrator` permission for its security and moderation features.
:::

## 1. Authorize Drew

Use the official Discord authorization flow:

[Add Drew to your server](https://discord.com/oauth2/authorize?client_id=1441457111409103010&permissions=8&integration_type=0&scope=bot+applications.commands)

## 2. Select the Server

Select the server where Drew should be installed.

You must have permission to manage the server and authorize applications.

## 3. Review Permissions

Confirm that `Administrator` is selected in the authorization screen.

:::danger Required Permission
Drew requires `Administrator` to operate its security, anti-raid, moderation, and Auto-Rollback functionality reliably.
:::

Do not remove required permissions after installation. Restricting Drew's effective permissions can prevent security actions from being executed correctly.

## 4. Complete Authorization

Approve the Discord authorization flow.

Discord may require additional verification, such as a CAPTCHA, before completing the installation.

Once authorization succeeds, return to your server.

## 5. Verify the Installation

Confirm that:

- Drew appears in the server member list.
- Drew's role has been created.
- Drew's role is positioned appropriately in the server hierarchy.
- Drew can access the channel where you intend to configure and test it.
- Drew can send messages and read message history where required.

:::success Installation Complete
If all checks pass, Drew is installed successfully and ready for configuration.
:::

Continue with [Module Setup](../commands/sec/init.md) to configure Drew's security modules.

If Drew is present but does not respond or cannot perform an action, see the [Troubleshooting Guide](../guides/troubleshooting.md).
