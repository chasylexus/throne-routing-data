# Trust Tunnel iOS Lists

These helper files flatten your current rules into simple lists for Trust Tunnel on iOS:

- `proxy-domains.txt` = put into `Vpn`
- `direct-domains.txt` = put into `Bypass`
- `excluded-routes.txt` = put into `Excluded routes`

What is included:

- `proxy-domains.txt` merges `A` and `T` on purpose.
- `proxy-domains.txt` and `direct-domains.txt` are built from both:
  - this repo's manual `Throne` rule-sets
  - the neighboring router repo's client-side lists `c-A-domains.txt`, `c-T-domains.txt`, `c-D-domains.txt`

What is intentionally not included:

- router-only `r-*` lists
- `domain_keyword` rules
- `ip_cidr` rules from the `Throne` repo
- nft-only `c-*-dst-v4.txt` advanced IP fallback lists

`excluded-routes.txt` mirrors the practical TUN exclusions from the working Surge profile.

Trust Tunnel rule syntax notes from the upstream client docs:

- `example.com` matches `example.com` and `www.example.com`
- `*.example.com` matches subdomains only, not the root domain itself
- IPs and CIDRs are supported too, but these helper files focus on domain-level routing

Practical use:

- `Vpn` => `proxy-domains.txt`
- `Bypass` => `direct-domains.txt`
- `Excluded routes` => `excluded-routes.txt`
