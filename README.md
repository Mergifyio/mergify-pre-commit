## Mergify pre-commit hook

Official pre-commit hooks for Mergify. Validate Mergify configuration files.

### Usage

Add the following to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/Mergifyio/mergify-pre-commit
    rev: 1.1.0
    hooks:
      - id: validate-mergify-config-location
      - id: validate-mergify-config
```

### validate-mergify-config

Validate Mergify configuration files against the official schema.

- Uses `check-jsonschema` with Mergify's schema: `https://docs.mergify.com/mergify-configuration-schema.json`
- Targets files matching the hook's `files` pattern.

Customization example (pass extra args to `check-jsonschema`):

```yaml
repos:
  - repo: https://github.com/Mergifyio/mergify-pre-commit
    rev: 1.1.0
    hooks:
      - id: validate-mergify-config
        args: ["--verbose"]
```

### validate-mergify-config-location

Ensure exactly one Mergify configuration file exists in an allowed location.

- Allowed locations (yml only):
  - `.mergify.yml`
  - `.mergify/config.yml`
  - `.github/mergify.yml`
- Runs as a system shell script, checks repo state (not just staged files).