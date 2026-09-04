---
label: Introduction
icon: light-bulb
order: 1
---

# Introduction

Drew is a security and moderation platform for Discord servers, designed to protect critical server resources, detect potentially destructive activity, and respond according to your configured security policies.

Before deploying Drew, review the following prerequisites:

- You have `Administrator` permission in the target server.
- You understand that Drew requires elevated permissions to perform security and moderation actions reliably.
- You have identified whether the server is a production or testing environment.
- You have a private channel available for initial configuration and validation.
- Drew's role can be positioned appropriately within the server hierarchy.
- Any external services required by the features you intend to use are available and correctly configured.

:::warning Production Deployment
Do not deploy security automation to a production server without first validating its permissions, role hierarchy, module configuration, whitelists, and expected enforcement behavior.
:::

:::info Recommended Approach
Start with a controlled configuration, validate Drew's behavior against expected events, and only then expand its protection across the server.
:::

Once the prerequisites have been verified, continue with [Installation](installation.md).
