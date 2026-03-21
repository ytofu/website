# Enabled Meta-Argument

The `enabled` meta-argument provides a simple way to conditionally create or skip a resource. It's an alternative to `count` for zero-or-one resource patterns.

## Overview

Sometimes you need to optionally create a resource based on a condition. While `count` can achieve this, `enabled` provides clearer intent:

```hcl
resource "aws_cloudwatch_log_group" "app" {
  name = "/app/logs"

  lifecycle {
    enabled = var.enable_logging
  }
}
```

## Basic Usage

Use `enabled` in the `lifecycle` block:

```hcl
variable "create_backup" {
  type    = bool
  default = false
}

resource "aws_db_instance" "backup" {
  identifier = "backup-db"
  # ... other configuration ...

  lifecycle {
    enabled = var.create_backup
  }
}
```

When `var.create_backup` is `false`, the resource is not created.

## Comparison with Count

### Using Count (Traditional)

```hcl
resource "aws_instance" "optional" {
  count = var.create_instance ? 1 : 0

  ami           = "ami-12345678"
  instance_type = "t3.micro"
}

# Reference requires index
output "instance_id" {
  value = var.create_instance ? aws_instance.optional[0].id : null
}
```

### Using Enabled (Simpler)

```hcl
resource "aws_instance" "optional" {
  ami           = "ami-12345678"
  instance_type = "t3.micro"

  lifecycle {
    enabled = var.create_instance
  }
}

# Direct reference
output "instance_id" {
  value = aws_instance.optional.id
}
```

## Benefits of Enabled

1. **Clearer intent** - Immediately obvious the resource is optional
2. **No index syntax** - Reference resources directly without `[0]`
3. **Simpler conditions** - Boolean variable instead of ternary expression
4. **Works in YAML** - Unlike `count`, `enabled` works in ytofu YAML files

## Using with YAML

In YAML configurations, use `enabled` since `count` is not supported:

```yaml
resource:
  aws_cloudwatch_log_group:
    app:
      name: /app/logs
      lifecycle:
        enabled: ${var.enable_logging}
```

## Use Cases

### Feature Flags

Enable resources based on feature configuration:

```hcl
variable "features" {
  type = object({
    monitoring = bool
    backups    = bool
    cdn        = bool
  })
}

resource "aws_cloudwatch_dashboard" "main" {
  dashboard_name = "app-dashboard"
  # ...

  lifecycle {
    enabled = var.features.monitoring
  }
}

resource "aws_backup_plan" "main" {
  name = "daily-backup"
  # ...

  lifecycle {
    enabled = var.features.backups
  }
}
```

### Environment-Specific Resources

Create resources only in certain environments:

```hcl
variable "environment" {
  type = string
}

resource "aws_waf_web_acl" "main" {
  name = "production-waf"
  # ...

  lifecycle {
    enabled = var.environment == "production"
  }
}
```

### Optional Integrations

Enable optional third-party integrations:

```hcl
variable "datadog_enabled" {
  type    = bool
  default = false
}

resource "datadog_monitor" "app" {
  name = "App Health Monitor"
  # ...

  lifecycle {
    enabled = var.datadog_enabled
  }
}
```

## Combining with Other Lifecycle Arguments

`enabled` works alongside other lifecycle arguments:

```hcl
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = "t3.micro"

  lifecycle {
    enabled               = var.create_instance
    create_before_destroy = true
    prevent_destroy       = var.environment == "production"
    ignore_changes        = [tags]
  }
}
```

## Limitations

1. **Boolean only** - Unlike `count`, `enabled` only accepts `true` or `false`
2. **Zero or one** - Cannot create multiple instances (use `count` or `for_each` in HCL for that)
3. **HCL lifecycle block** - Must be defined within a `lifecycle` block

## When to Use Each

| Scenario | Use |
|----------|-----|
| Optional single resource | `enabled` |
| Multiple identical resources | `count` (HCL only) |
| Resources from a map/set | `for_each` (HCL only) |
| YAML optional resource | `enabled` |

## Migration from Count

Convert `count = condition ? 1 : 0` to `enabled`:

**Before (HCL with count)**
```hcl
resource "aws_instance" "web" {
  count = var.create ? 1 : 0
  # ...
}

# References need [0]
output "id" {
  value = var.create ? aws_instance.web[0].id : null
}
```

**After (with enabled)**
```hcl
resource "aws_instance" "web" {
  # ...
  lifecycle {
    enabled = var.create
  }
}

# Direct reference
output "id" {
  value = aws_instance.web.id
}
```

Note: This changes how the resource is addressed in state. Plan carefully when migrating existing resources.

## Related

- [Configuration as Data](configuration-as-data.md)
- [Resource Lifecycle](resource-lifecycle.md)
- [YAML vs HCL](yaml-vs-hcl.md)
