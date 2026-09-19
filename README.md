# Private Paper Bots Scheduler

This public repository contains only a free GitHub Actions scheduler. It calls
the workflows in two private, paper-only strategy repositories. No strategy
source, parameters, signal history, position state, Telegram token, or chat ID
is copied into this public repository.

## One required Actions secret

Under **Settings → Secrets and variables → Actions**, add:

- `PRIVATE_REPO_TOKEN`: a fine-grained personal access token limited to
  `leekyuan/btc-15-min-ote-strategy` and `leekyuan/btc-4h-signal-bot`, with
  **Actions: Read and write** and **Metadata: Read-only** permissions.

The private workflows continue to use their own existing Telegram secrets and
their own repository-scoped `GITHUB_TOKEN` when saving paper state.

## Schedule

The public scheduler runs at minutes `06`, `21`, `36`, and `51` each
hour. It dispatches the private 15-minute monitor every run and the private
4-hour monitor, which exits without an alert when no new 4-hour close is due.
A daily public heartbeat commit prevents inactivity-based schedule disabling.

Actual exchange orders remain disabled.
