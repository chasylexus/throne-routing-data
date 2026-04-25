# throne-routing-data

Minimal hand-edited routing data repo for `Throne`.

This repo is intentionally simple:

- you edit JSON files by hand on GitHub
- `Throne` fetches those JSON files as `remote rule_set`
- `Throne` refreshes them on schedule with `update_interval: "2h"`

There is no build step in the normal workflow.

## Files You Usually Edit

Most changes should happen only in these files:

- `rule-set/manual-d.json`
- `rule-set/manual-a.json`
- `rule-set/manual-t.json`

Meaning:

- `manual-d` = direct exceptions
- `manual-a` = outbound `A`
- `manual-t` = outbound `T`

## Files For Throne

`Throne` configuration lives in `throne/`:

- `throne/custom-config.template.json`
- `throne/custom-config.ipv4-only.template.json`
- `throne/route.rule_set.json`
- `throne/route.rules.json`
- `throne/route.inline-rules.json`

`throne/custom-config.template.json` is the main dual-stack profile and uses DNS through the matching proxy outbound for `A` and `T`.

`throne/custom-config.ipv4-only.template.json` is the fallback comparison profile. It uses the same proxy-side DNS behavior, but keeps internet traffic IPv4-only.

The current configured rule-set base URL is:

`https://raw.githubusercontent.com/chasylexus/throne-routing-data/main/rule-set`

Then `Throne` will fetch:

- `https://raw.githubusercontent.com/chasylexus/throne-routing-data/main/rule-set/manual-d.json`
- `https://raw.githubusercontent.com/chasylexus/throne-routing-data/main/rule-set/manual-a.json`
- `https://raw.githubusercontent.com/chasylexus/throne-routing-data/main/rule-set/manual-t.json`

## What Updates Automatically

If you commit changes to `rule-set/manual-*.json`, `Throne` will fetch the updated versions from the same URLs on its next refresh interval.

That means:

- adding domains to `manual-t.json` updates proxy rules automatically
- adding IP or CIDR to `manual-d.json` updates direct rules automatically
- moving items between `manual-a.json` and `manual-t.json` updates behavior automatically

## What Does Not Update Automatically

The list of referenced upstream tags inside the local `Throne` `Custom Config` is still static.

So if you later want to:

- add a brand new upstream rule-set tag
- remove an upstream rule-set tag
- reorder the route groups

you must also update the local `Throne` config.

## Safety

- Do not store credentials, tokens, passwords, private hostnames, or personal data here.
- Do not store files that reveal a user name, family name, or organization.
- Use a neutral GitHub owner if the repo will be public.
