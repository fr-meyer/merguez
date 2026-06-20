# Mergeguez

Mergeguez is a GitHub automation bot for owner-approved development workflows.

It uses host-side, least-privilege brokered credentials to prepare branches, open pull requests, update project surfaces, and publish approved releases without storing personal GitHub credentials in the runtime environment.

## What It Does

- Prepares and pushes approved branches for selected repositories.
- Opens and updates pull requests for reviewed work.
- Updates GitHub Project surfaces when the workflow explicitly allows it.
- Prepares approved release and tag operations where a repository has opted in.

Mergeguez is not a general-purpose GitHub administrator. It runs a small set of allowlisted operations for selected repositories and workflows.

## Security Model

- Personal GitHub credentials are not stored in the automation runtime.
- GitHub write access is brokered from the host side through explicit, narrow commands.
- GitHub App installation tokens are short-lived.
- Repository and operation allowlists limit what each workflow can touch.
- Public writes, releases, and tags require human approval before execution.

## Permissions

The exact installation can vary by repository, but Mergeguez should use the smallest practical permission set for the enabled workflows:

- Metadata: read-only repository discovery.
- Contents: write access only where branch or release preparation is enabled.
- Pull requests: write access where pull request creation or updates are enabled.
- Issues and Projects: only where project tracking or issue workflow integration is explicitly configured.

Mergeguez should not request broad administrative, secrets, or organization-wide permissions unless a future workflow has a clear, reviewed need for them.

## Privacy

Mergeguez should publish only repository content that has passed the intended preflight checks. It should not log, commit, or expose access tokens, private keys, personal credentials, or private runtime configuration.

When a workflow needs private context, that context stays in the private automation environment unless the owner explicitly approves a public artifact.

## Name

The name is a small French and Git joke: "Mergeguez" blends merge work with merguez, while also nodding to the French slang use of merguez for something a bit sketchy or botched. The bot's job is to help keep agent-generated work from becoming merguez-code.
