# Resource Lifecycle

Understand how ytofu manages resources through their lifecycle.

## Overview

ytofu manages resources through a simple lifecycle:

```
┌─────────┐     ┌─────────┐     ┌─────────┐
│  Plan   │ ──▶ │  Apply  │ ──▶ │ Destroy │
└─────────┘     └─────────┘     └─────────┘
```

## Commands

### ytofu init

Initialize a working directory containing ytofu configuration files.

```bash
ytofu init
```

This command:
- Downloads required providers
- Initializes the backend
- Prepares the working directory

### ytofu plan

Preview changes that will be made to your infrastructure.

```bash
ytofu plan
```

Output shows:
- Resources to be created (`+`)
- Resources to be modified (`~`)
- Resources to be destroyed (`-`)

Example output:
```
Terraform will perform the following actions:

  # aws_instance.web will be created
  + resource "aws_instance" "web" {
      + ami           = "ami-0c55b159cbfafe1f0"
      + instance_type = "t3.micro"
      + tags          = {
          + "Name" = "web-server"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
```

### ytofu apply

Apply the changes to create, update, or destroy resources.

```bash
ytofu apply
```

This command:
- Shows the plan (like `ytofu plan`)
- Asks for confirmation
- Makes changes to infrastructure
- Updates the state file

### ytofu destroy

Destroy all resources managed by the configuration.

```bash
ytofu destroy
```

Use with caution - this removes all resources.

## State Management

ytofu tracks resources using a **state file** (`terraform.tfstate`).

### What State Contains

- Resource IDs and attributes
- Dependencies between resources
- Provider configurations
- Metadata

### State Location

By default, state is stored locally. For teams, use remote backends:

```yaml
terraform:
  backend:
    s3:
      bucket: my-terraform-state
      key: prod/terraform.tfstate
      region: us-west-2
```

## Resource Operations

### Create

When a resource exists in configuration but not in state:

```yaml
# New resource - will be created
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
```

### Update

When a resource exists in both configuration and state, but attributes differ:

```yaml
# Changed attribute - will be updated
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.large  # Changed from t3.micro
```

Some changes require **replacement** (destroy + create):
- Changing AMI
- Changing subnet
- Changing availability zone

### Destroy

When a resource exists in state but not in configuration:

```yaml
# Resource removed from configuration
# The aws_instance.web resource will be destroyed
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16
  # aws_instance.web was here, now removed
```

## Dependencies

ytofu automatically handles dependencies based on resource references.

### Implicit Dependencies

```yaml
resource:
  aws_vpc:
    main:
      cidr_block: 10.0.0.0/16

  aws_subnet:
    public:
      vpc_id: ${aws_vpc.main.id}  # Depends on VPC
      cidr_block: 10.0.1.0/24
```

The subnet depends on the VPC because it references `${aws_vpc.main.id}`.

### Explicit Dependencies

Use `depends_on` for dependencies that aren't visible through references:

```yaml
resource:
  aws_nat_gateway:
    main:
      allocation_id: ${aws_eip.nat.id}
      subnet_id: ${aws_subnet.public.id}
      depends_on:
        - aws_internet_gateway.main  # Explicit dependency
```

## Lifecycle Customization

Control resource behavior with lifecycle settings:

```yaml
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      lifecycle:
        create_before_destroy: true
        prevent_destroy: true
        ignore_changes:
          - tags
```

### Options

| Option | Description |
|--------|-------------|
| `create_before_destroy` | Create replacement before destroying original |
| `prevent_destroy` | Prevent accidental destruction |
| `ignore_changes` | Don't update specified attributes |
| `replace_triggered_by` | Replace when referenced resources change |

## Workflow Example

1. **Write configuration**
   ```yaml
   resource:
     aws_instance:
       web:
         ami: ami-0c55b159cbfafe1f0
         instance_type: t3.micro
   ```

2. **Initialize**
   ```bash
   ytofu init
   ```

3. **Preview changes**
   ```bash
   ytofu plan
   ```

4. **Apply changes**
   ```bash
   ytofu apply
   ```

5. **Modify configuration**
   ```yaml
   resource:
     aws_instance:
       web:
         ami: ami-0c55b159cbfafe1f0
         instance_type: t3.large  # Changed
   ```

6. **Apply updates**
   ```bash
   ytofu plan   # See what changes
   ytofu apply  # Apply changes
   ```

7. **Destroy when done**
   ```bash
   ytofu destroy
   ```

## Best Practices

- **Always run plan first** - Review changes before applying
- **Use remote state** - Enable team collaboration
- **Lock state** - Prevent concurrent modifications
- **Version control** - Track configuration changes in git
- **Small changes** - Apply incremental updates
- **Backup state** - Protect against data loss

## Related

- [Configuration as Data](configuration-as-data.md)
- [YAML vs HCL](yaml-vs-hcl.md)
- [Getting Started](../getting-started.md)
