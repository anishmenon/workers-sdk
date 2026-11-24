---
"@cloudflare/workers-auth": patch
"wrangler": patch
---

Fix auth profiles bound to the filesystem root never being applied

`wrangler auth activate <name> /` (or `--cwd=/`) stored the binding but it was only matched for `/` itself, so it never applied to any real directory. The path-boundary check required the character after the bound directory to be a separator, which can never hold when the bound directory already ends with one (`/`, `C:\`). A root binding now acts as the global fallback for every directory that has no more specific binding, as intended.
