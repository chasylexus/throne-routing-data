# Editing Guide

## Normal Workflow

For day-to-day routing changes, edit only one of these files:

- `rule-set/manual-d.json`
- `rule-set/manual-a.json`
- `rule-set/manual-t.json`

Then commit the change in GitHub's web UI.

`Throne` will keep fetching the same file URL and will pick up the new content on the next `2h` refresh.

## Which File To Choose

- `manual-d.json`: domains or IPs that must stay direct
- `manual-a.json`: domains or IPs that must go to outbound `A`
- `manual-t.json`: domains or IPs that must go to outbound `T`

## Valid Rule Fields

Inside these files, use only sing-box headless rule fields that are relevant here:

- `domain`
- `domain_suffix`
- `domain_keyword`
- `ip_cidr`

## Comments Are Allowed

These `manual-*.json` files may contain comments.

Safe comment styles:

- `// single line`
- `# single line`
- `/* multi-line */`

That works because sing-box parses source rule-set JSON through its extended JSON reader with a comment filter.

## Editing Examples

Add one exact domain:

```json
{
  "domain": [
    "example.com"
  ]
}
```

Add one suffix:

```json
{
  "domain_suffix": [
    "example.org"
  ]
}
```

Add IP and CIDR:

```json
{
  "ip_cidr": [
    "203.0.113.10",
    "198.51.100.0/24"
  ]
}
```

## Important JSON Notes

- Keep valid JSON syntax.
- Use double quotes.
- Do not leave trailing commas.
- Keep the top-level structure as `{"version": 1, "rules": [...]}`.
- Keep the four fixed sections in the existing order so future edits stay easy to scan.

## Less Common Edits

Only edit these if the static `Throne` wiring itself changes:

- `throne/route.rule_set.json`
- `throne/route.rules.json`
- `throne/custom-config.template.json`
