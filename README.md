# Docue for Claude

![Docue](assets/icon.png)

Find documents, create drafts, and manage signing in [Docue](https://docue.com) from Claude chat, Cowork, and Claude Code.

## What you can do

- **Find and read:** locate contracts, summarize their terms, and compare documents with links to the sources.
- **Draft and edit:** create an editable draft from a compatible Builder 2 template and update its sections using the facts you provide.
- **Manage signing:** review signees, finalize drafts, check signing progress, and manage invitations and settings when requested.
- **Organize documents:** manage folders and the archive, including deleting documents or folders when requested.

For example, ask Claude to “Find the NDA with Acme and summarize its termination terms,” “Create an English NDA draft using the party details I provide,” or “Check who still needs to sign this document.”

You need a Docue account, an eligible workspace subscription, and permission for the requested action. Builder editing is available for editable Builder 2 drafts. Each signee must complete their own signature and any required identity verification. Review drafts and summaries before relying on them for legal decisions or finalizing a document.

## Install and connect

### Claude chat and Cowork

1. Find **Docue** in Claude's plugin marketplace and add the plugin.
2. Open the plugin's **Connectors** tab, connect Docue, and complete sign-in.

On Team and Enterprise plans, an organization Owner may need to add the connector before members can connect their own accounts. Installing the plugin alone does not connect your Docue account.

### Claude Code

Use `/plugin` to find and install Docue from the marketplace, or manage an installation synced from your Claude account. Use `/mcp` to check the connection and sign in.

Claude can select the included skills automatically, or you can invoke `/docue:find-documents`, `/docue:create-builder-document`, or `/docue:manage-document-signing`.

## Troubleshooting

If the connector is missing or sign-in fails, check the plugin’s **Connectors** tab in Claude chat or Cowork, or use `/mcp` in Claude Code to check the connection and sign in again. On Team and Enterprise plans, an organization Owner may need to add the connector. For access or permission errors, check that your connected Docue account has the required workspace and document permissions; reconnecting does not grant additional access.

## Permissions

The connector follows the permissions of your connected Docue account. Your existing workspace and document permissions determine what Claude can access and which actions it can perform. Claude's tool permissions also apply.

## Privacy and support

Claude exchanges tool requests and results with Docue's hosted MCP server at `https://mcp.docue.com`; sign-in uses `https://auth.docue.com`. Depending on your request, data may include document text, metadata, workspace information, and party or signee contact details. Requested changes are saved in Docue, and requested emails, invitations, and reminders may be delivered through Docue's services. Tool results become part of your Claude conversation.

The plugin runs no local server or hooks, installs no dependencies, and adds no analytics or separate data store. See Docue's [privacy statement](https://docue.com/en/privacy) and [terms of use](https://docue.com/en/terms); Claude's account terms and privacy settings also apply. The [MIT license](LICENSE) covers the plugin files, not access to Docue's service or templates.

For service support, [contact Docue](https://docue.com/en/contact) or email support@docue.com. Report plugin problems in [GitHub issues](https://github.com/docue/claude-plugin/issues) using synthetic examples. Do not post passwords, OAuth tokens, signing links, PINs, or customer documents in public issues.
