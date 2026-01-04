# Concepts

Understand the core principles and philosophy behind ytofu.

## What is ytofu?

ytofu is an OpenTofu fork with first-class YAML support. It brings the **Configuration as Data** paradigm to infrastructure management, allowing you to define your infrastructure using YAML instead of HCL.

## Core Concepts

| Concept | Description |
|---------|-------------|
| [Configuration as Data](configuration-as-data.md) | Infrastructure defined as pure data, not code |
| [YAML vs HCL](yaml-vs-hcl.md) | Understanding the differences and benefits |
| [Resource Lifecycle](resource-lifecycle.md) | How resources are created, updated, and destroyed |

## Why Configuration as Data?

Traditional Infrastructure as Code (IaC) tools mix data with logic - variables, loops, conditionals, and functions. This makes configurations:

- **Hard to read** - Logic intertwined with data
- **Hard to generate** - Complex to produce programmatically
- **Hard to audit** - Difficult to verify what actually gets deployed

ytofu takes a different approach: **pure data, no logic**.

```yaml
# What you write is what you deploy
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      tags:
        Name: web-server
```

## Learning Path

1. **Start here**: [Getting Started](../getting-started.md) - Install ytofu and deploy your first resource
2. **Understand the philosophy**: [Configuration as Data](configuration-as-data.md)
3. **Learn by doing**: [Tutorials](../tutorials/index.md)
4. **Solve specific problems**: [Guides](../guides/index.md)
5. **Reference documentation**: [AWS Resources](../aws/index.md)
