# Troubleshooting

Solutions to common ytofu issues and error messages.

## Quick Links

| Category | Description |
|----------|-------------|
| [Common Errors](common-errors.md) | Error messages and solutions |

## General Troubleshooting Steps

### 1. Check ytofu Version

```bash
ytofu version
```

Ensure you're running a recent version.

### 2. Reinitialize

Many issues are resolved by reinitializing:

```bash
rm -rf .terraform
ytofu init
```

### 3. Check State

Inspect the current state:

```bash
ytofu state list
ytofu state show <resource>
```

### 4. Enable Debug Logging

Get detailed logs:

```bash
TF_LOG=DEBUG ytofu plan
```

Log levels: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`

### 5. Validate Configuration

Check for syntax errors:

```bash
ytofu validate
```

## Common Categories

### Initialization Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| Provider not found | Missing init | Run `ytofu init` |
| Backend error | Credentials issue | Check AWS credentials |
| Version constraint | Incompatible version | Update version constraints |

### Plan/Apply Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| Resource not found | Deleted outside ytofu | Run `ytofu refresh` |
| Dependency cycle | Circular references | Review resource dependencies |
| Timeout | API rate limiting | Add retry logic or wait |

### State Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| State lock | Concurrent operation | Wait or force unlock |
| State mismatch | Manual changes | Run `ytofu refresh` |
| Corrupted state | File corruption | Restore from backup |

## Getting Help

If you can't resolve an issue:

1. **Search existing issues** on GitHub
2. **Check AWS status** for service outages
3. **Review documentation** for the specific resource
4. **Open an issue** with detailed reproduction steps

## Related

- [Common Errors](common-errors.md)
- [Resource Lifecycle](../concepts/resource-lifecycle.md)
- [Getting Started](../getting-started.md)
