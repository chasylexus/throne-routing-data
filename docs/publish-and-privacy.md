# Publish And Privacy

## Current Local Audit

Before any remote repository is created:

- no commits exist yet
- no GitHub remote is configured yet
- no secrets, passwords, tokens, UUIDs, hosts, or private outbound credentials are stored in this repo
- no hard-coded local filesystem paths with a personal name remain in tracked files

The local Git author configuration for this repo is pinned to neutral values:

- `user.name = router-maintainer`
- `user.email = router-maintainer@example.invalid`

## Main Privacy Risks

### 1. The GitHub owner path itself

The biggest remaining privacy risk is usually the public owner path:

- `github.com/<owner>/<repo>`
- `raw.githubusercontent.com/<owner>/<repo>/main/rule-set/manual-t.json`

If `<owner>` contains a real name or organization, the published rule-set URLs reveal it immediately.

### 2. Web UI commits belong to the GitHub account that makes them

If you edit files in GitHub's web interface, the commit is attributed to that GitHub account.
GitHub's docs say web-based operations use the account email settings, and with email privacy enabled the commit email becomes a GitHub no-reply address.

That protects the email address, but not the account identity itself.

### 3. Public profile fields

Even with a no-reply email, these can still reveal identity:

- username
- display name
- avatar
- bio
- organization
- linked website

## Recommended Safe Setup

Before creating the GitHub repo:

1. Use a neutral GitHub owner that does not reveal a real name or organization.
2. In GitHub Settings -> Emails, enable `Keep my email addresses private`.
3. In the same section, enable `Block command line pushes that expose my email`.
4. Keep the public profile itself neutral if you plan to edit in the web UI.
5. Use a public repository only if you are comfortable exposing the routing domain and IP lists themselves.

## Publishing Model

This repo is designed for direct publishing of the tracked JSON files.

Recommended URL shape:

`https://raw.githubusercontent.com/<owner>/<repo>/main/rule-set`

Then `Throne` can fetch:

- `.../manual-d.json`
- `.../manual-a.json`
- `.../manual-t.json`

## What You Normally Edit On GitHub

Usually only these files:

- `rule-set/manual-d.json`
- `rule-set/manual-a.json`
- `rule-set/manual-t.json`

Less often:

- `throne/custom-config.template.json`
- `throne/route.rule_set.json`
- `throne/route.rules.json`

Those `throne/` files only need edits when the static list of upstream rule-set tags changes.
