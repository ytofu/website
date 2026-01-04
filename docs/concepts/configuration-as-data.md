# Configuration as Data

ytofu follows the **Configuration as Data** (CaD) philosophy. Your infrastructure is defined as plain YAML data, not code.

## The Philosophy

Configuration as Data means:

- **No programming constructs** - No loops, conditionals, or functions
- **No variable substitution** - No `${var.xxx}` references
- **Explicit resources** - Every resource is defined individually
- **What you see is what you deploy** - No runtime evaluation

## What to Avoid

These programming constructs are **not used** in ytofu:

### No For Loops

```yaml
# AVOID: for expressions
resource:
  aws_subnet:
    public:
      for_each: ${toset(var.azs)}
      cidr_block: ${cidrsubnet(var.vpc_cidr, 8, each.key)}
```

### No Variables

```yaml
# AVOID: variable references
resource:
  aws_instance:
    web:
      instance_type: ${var.instance_type}
      ami: ${var.ami_id}
```

### No Functions

```yaml
# AVOID: function calls
resource:
  aws_subnet:
    public:
      cidr_block: ${cidrsubnet(aws_vpc.main.cidr_block, 8, 1)}
```

### No Conditionals

```yaml
# AVOID: conditional expressions
resource:
  aws_instance:
    web:
      instance_type: ${var.environment == "prod" ? "t3.large" : "t3.micro"}
```

## What to Use Instead

### Explicit Values

```yaml
# GOOD: Explicit values
resource:
  aws_instance:
    web:
      instance_type: t3.micro
      ami: ami-0c55b159cbfafe1f0
```

### Explicit Resources

```yaml
# GOOD: Each resource defined explicitly
resource:
  aws_subnet:
    public_a:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.1.0/24
      availability_zone: us-west-2a

    public_b:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.2.0/24
      availability_zone: us-west-2b

    public_c:
      vpc_id: ${aws_vpc.main.id}
      cidr_block: 10.0.3.0/24
      availability_zone: us-west-2c
```

### Simple Resource References

Resource references using `${resource_type.name.attribute}` are allowed because they represent relationships, not logic:

```yaml
# GOOD: Resource references for relationships
resource:
  aws_instance:
    web:
      subnet_id: ${aws_subnet.public_a.id}
      vpc_security_group_ids:
        - ${aws_security_group.web.id}
```

## Benefits of Configuration as Data

### Readable

Every value is explicit. No mental parsing of expressions or variable lookups.

```yaml
# You know exactly what will be deployed
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      tags:
        Environment: production
        Application: web
```

### Auditable

Easy to review and diff. Changes are visible in plain data.

```diff
 resource:
   aws_instance:
     web:
-      instance_type: t3.micro
+      instance_type: t3.large
```

### Generatable

Simple to produce from external tools. Any language can generate YAML.

```python
# Python script to generate ytofu config
import yaml

config = {
    'resource': {
        'aws_instance': {
            'web': {
                'ami': 'ami-0c55b159cbfafe1f0',
                'instance_type': 't3.micro'
            }
        }
    }
}

print(yaml.dump(config))
```

### GitOps-Ready

Works naturally with Kubernetes-style workflows. Apply, diff, sync.

```bash
# Apply changes
ytofu apply

# See what would change
ytofu plan
```

## Comparison Table

| Feature | Traditional IaC | ytofu (CaD) |
|---------|-----------------|-------------|
| Variables | `${var.name}` | Concrete values |
| Loops | `for_each`, `count` | Explicit resources |
| Conditionals | `condition ? a : b` | No conditionals |
| Functions | `cidrsubnet()`, `join()` | No functions |
| Dynamic blocks | `dynamic "block" {}` | Static definitions |
| Locals | `locals { }` | No locals |

## When to Use External Tools

If you need to generate multiple similar resources, use external tools:

1. **Generate YAML** with scripts (Python, Go, etc.)
2. **Template engines** like Jinja2 or Helm
3. **Configuration management** tools
4. **CI/CD pipelines** that produce YAML

The logic lives **outside** ytofu, keeping your configurations pure data.

## Related

- [YAML vs HCL](yaml-vs-hcl.md)
- [Resource Lifecycle](resource-lifecycle.md)
- [Getting Started](../getting-started.md)
