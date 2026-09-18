# ICIS Community Registry

Community-maintained package registry for [ICIS](https://github.com/icis-org/icis).

## How it works

- Each app is a single `.ici` file in `packages/`
- PRs are auto-validated and auto-merged when checks pass
- `registry.json` is auto-generated on every merge — never edit it by hand

## Add a package

1. **Fork** this repo
2. Create `packages/your-app.ici`:

```ini
name: Your App
version: 1.0
desc: Short description
url: https://example.com/your-app-1.0.zip
type: zip
install_dir: appdata
shortcuts: your-app.exe=Your App
startup: false
```

3. **Open a PR** — CI validates automatically
4. If checks pass → **auto-merged** → live in the Store within minutes

## `.ici` field reference

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique app name (lowercase, hyphens only) |
| `version` | No | Version string |
| `desc` | No | Short description |
| `url` | Yes | Download URL (https only) |
| `type` | No | Archive type: `zip` (default), `7z`, `rar`, `exe`, `msi` |
| `install_dir` | No | `appdata` (default), `programfiles`, `custom` |
| `custom_dir` | No | Path when `install_dir: custom` |
| `shortcuts` | No | Comma-separated: `exe.exe=Display Name` |
| `startup` | No | `true` to add to Windows Startup |
| `icon` | No | Icon path inside the archive |
| `homepage` | No | Project homepage URL |

## Validation rules

- `name` and `url` are required
- `url` must be `https://` (no http, no local paths)
- `name` must be `[a-z0-9-]` only
- No duplicate `name` values across the registry
- `shortcuts:` exe paths cannot use `..` or absolute paths
- Only `packages/*.ici` files are accepted in PRs
- Max 5 new packages per PR

## License

Package metadata is public domain. The apps themselves retain their original licenses.
