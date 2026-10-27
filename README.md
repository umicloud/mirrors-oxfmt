# mirrors-oxfmt

This repository is a [pre-commit](https://pre-commit.com/) mirror for the npm package `oxfmt`.

It is not the source code for `oxfmt`.  
Its job is to publish and maintain the files/tags needed so users can run `oxfmt` via `pre-commit`.

## Usage
### pre-commit
```yaml
- repo: https://github.com/umicloud/mirrors-oxfmt
  rev: "v0.75.0" # Use the sha / tag you want to point at
  hooks:
    - id: oxfmt
    - id: oxfmt-check
```

### prek
```toml
[[repos]]
repo = "https://github.com/umicloud/mirrors-oxfmt"
rev = "v0.75.0" # Use the sha / tag you want to point at
hooks = [
  { id = "oxfmt" },
  { id = "oxfmt-check" },
]
```

## How it works

- `.github/workflows/main.yml` runs `pre-commit-mirror-maker` on pushes to `main` and opens a mirror update PR.
- `.pre-commit-hooks.yaml` defines the hook metadata (`id`, `entry`, dependency version, file types).
- `.version` stores the currently mirrored package version.

The workflow regenerates mirror content, pushes missing tags, and opens an auto-merge PR for mirror updates.

## Updating

When a new `oxfmt` release should be mirrored:

1. Update `.version` to that npm version.
2. Keep `.pre-commit-hooks.yaml` `additional_dependencies` aligned with the same version.
3. Push to `main` to run the workflow and open the mirror update PR.
