# 0magnet/go-colorful

A fork of [lucasb-eyer/go-colorful](https://github.com/lucasb-eyer/go-colorful).

## Branches

| branch | module path | what it is |
| --- | --- | --- |
| `upstream` | `github.com/lucasb-eyer/go-colorful` | an exact mirror of upstream's default branch, never modified |
| `master` | `github.com/0magnet/go-colorful` | what other repos import: every fix below, plus the module rename |
| `no-database-sql` | `github.com/lucasb-eyer/go-colorful` | one fix, based on `upstream`, shaped for a pull request |

A fix lands on its own branch off `upstream` first, so it can be offered
upstream unchanged, and is then merged into `master`. `master` differs from the
sum of those branches only by the module path.

## Fixes carried here

- **`no-database-sql`** — `HexColor.Value` returns `driver.Value`, and that one
  return type pulls `database/sql/driver` → `uuid` → `crypto/rand` →
  `crypto/fips140`: 26 crypto packages and 169KB of a 3.2MB js/wasm binary,
  for an interface neither js/wasm nor TinyGo can use. The methods move behind
  `!tinygo && !js`.
