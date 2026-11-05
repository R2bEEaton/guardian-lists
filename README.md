# guardian-lists

Signed, hashed domain lists for the Guardian self-accountability app. The app downloads `domains.gdl` and
`domains.gdl.sig` from this repository about once a week and installs them only if the Ed25519 signature verifies
against the public key built into the app and the version number is higher than the one it already has.

## What is in here

| File | What it is |
|---|---|
| `domains.gdl` | The list. Format `GDL1`: a small header, then sorted 8-byte prefixes of the SHA-256 of each domain name. It contains **no readable domain names** and cannot be turned back into a list of sites. |
| `domains.gdl.sig` | Detached Ed25519 signature over `domains.gdl` (64 raw bytes). |
| `domains.gdl.manifest.json` | Version, number of entries, SHA-256 of the file and the sources it was built from. |
| `public_key.hex` | The public half of the signing key (same value as in the app). |

Verify by hand: `python scripts/verify_blocklist.py --list domains.gdl --pub public_key.hex` (script in the main project).

## Where the entries come from

Built by the project's `build_blocklist.py` from public adult-domain lists (see `domains.gdl.manifest.json` for the exact
sources and counts). The current source is the `porn` extension of
[StevenBlack/hosts](https://github.com/StevenBlack/hosts) (MIT licensed), which itself merges several upstream lists,
among them [hostsVN](https://github.com/bigdargon/hostsVN) (Adult), [Clefspeare13/pornhosts](https://github.com/Clefspeare13/pornhosts)
(MIT) and others, each with its own terms. Domain names are facts and only truncated hashes of them are published here,
but if you maintain one of these lists and object, open an issue and the affected entries will be removed.

## No warranty

This list is a best-effort aid for a personal accountability tool. It will miss sites and may include a few it should not.
It is not a safety or compliance product.
