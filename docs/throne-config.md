# Throne Config

## Recommended Files

Use these files as the source for the local `Throne` `Custom Config` setup:

- `throne/custom-config.template.json`
- `throne/custom-config.local-dns.template.json`
- `throne/route.rule_set.json`
- `throne/route.rules.json`
- `throne/route.inline-rules.json`

## Profile Variants

There are now two local profile templates that point to the same GitHub-hosted rule-set assets:

- `throne/custom-config.template.json`
  This is now the main profile. It sends DNS for `manual-a`/`netflix` through outbound `A` and DNS for `manual-t` plus the upstream `T` tags through outbound `T`.
  Use this when domains correctly match `A` or `T`, and you want DNS resolution to happen from the proxy side instead of the local network side.
- `throne/custom-config.local-dns.template.json`
  This is the fallback comparison profile. It keeps the older behavior where DNS resolution stays local, and the rule-sets only decide which outbound is used later.

## Clash UI Noise

Both templates now also include a minimal local Clash API listener at `127.0.0.1:9090`.
This is not used for routing itself, but it helps `Throne` stop printing repeated `no clash server found` messages when its UI tries to list active connections for a custom profile.

## What To Replace

The rule-set base URL is already configured as:

`https://raw.githubusercontent.com/chasylexus/throne-routing-data/main/rule-set`

You still need to replace outbound placeholders such as:

- `__T_HOST__`, `__T_UUID__`, `__T_FINGERPRINT__`
- `__A_HOST__`, `__A_UUID__`, `__A_FINGERPRINT__`

## What Updates On Schedule

These remote rule-sets are designed to update every `2h`:

- `manual-d`
- `manual-a`
- `manual-t`

So after a GitHub web edit and commit to one of:

- `rule-set/manual-d.json`
- `rule-set/manual-a.json`
- `rule-set/manual-t.json`

`Throne` will fetch the updated file on its next rule-set refresh cycle.

## What Usually Needs No Further Local Edits

If you only change domains, IPs, or CIDRs inside the three manual files, you usually do not need to touch the local `Throne` config again.

## When You Do Need To Touch Local Throne Config Again

You must update the local `Throne` config if you want to:

- change the list of upstream remote tags
- change the outbound priority order
- add new inline-only rules
- change the base URL or branch path
