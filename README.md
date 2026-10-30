# PR Board

One page for every open pull request you wrote and every PR waiting on your review, across all the repos you can access. Tag each PR with your own status, like "Testing pending by me", and add a note to yourself.

There is no backend. It's a single static page (`index.html`) that runs in your browser and talks directly to the GitHub API.

## Use it

Open the published page, or open `index.html` from a local copy, then paste a GitHub token.

**Which token**

- **PRs in one org:** a [fine-grained token](https://github.com/settings/personal-access-tokens/new) with that org as resource owner and all repositories selected. Set *Pull requests* to read-only and, under account permissions, *Gists* to read and write. *Metadata* is added automatically. The org may need to approve the token.
- **PRs in several orgs:** a [classic token](https://github.com/settings/tokens/new?scopes=repo,gist&description=PR%20Board) with the `repo` and `gist` scopes. GitHub has no read-only version of `repo`, so this token can also write to your repos, even though the board never does. If an org uses SSO, authorize the token for it.

## Where your data lives

| Data | Location |
|---|---|
| GitHub token | This browser's local storage. Sent only to `api.github.com`. |
| Statuses, custom statuses, notes, PRs added by link | A secret gist named `pr-board-status.json` in your own GitHub account. |
| Cached PR list, filters | This browser's local storage. |

Nobody who hosts or publishes this page can see your token or your data.

A secret gist is unlisted, not access-controlled: anyone who has its link can read it. Don't share the link.

Remove the token with **Statuses & settings → Forget token on this browser**, and revoke it on GitHub when you stop using the board.

## Known limits

- Each list loads up to 100 open PRs, and closed PRs load up to 500 per date range.
- Saves overwrite the whole gist. If two devices edit within a few minutes of each other, the later save can undo the earlier one.
- If you publish this on `<you>.github.io`, every Pages site under that account shares browser storage, so other pages you host there could read a saved token. Only host pages you trust under the same account.
