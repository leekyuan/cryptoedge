# Private Paper Bots Runtime

This public repository contains only the free GitHub Actions scheduler for two
private, paper-only monitoring systems.

The strategy source, parameters, position state, signal history, and failure
details stay in the private repositories. The public workflow does not place
exchange orders and never enables live trading.

## Required Actions secrets

Add these under **Settings → Secrets and variables → Actions**:

- `PRIVATE_REPO_TOKEN`: fine-grained personal access token limited to the two
  private strategy repositories, with **Contents: Read and write** only.
- `PRIVATE_15M_REPOSITORY`: full name of the private 15-minute repository.
- `PRIVATE_4H_REPOSITORY`: full name of the private 4-hour repository.
- `TELEGRAM_BOT_TOKEN`: token for the existing Telegram alert bot.
- `TELEGRAM_CHAT_ID`: destination chat ID used by the existing bot.

Do not store these values in repository files or Actions variables.

## Schedule

The runner starts at minutes `06`, `21`, `36`, and `51` every hour. The 15-minute
monitor catches up missed closed candles. The 4-hour monitor runs only when a new
4-hour cycle is due. A daily public heartbeat commit prevents GitHub from
automatically disabling an inactive scheduled workflow.
