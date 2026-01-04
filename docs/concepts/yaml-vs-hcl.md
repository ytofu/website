# YAML vs HCL

Compare ytofu's YAML format with traditional Terraform HCL.

## Syntax Comparison

### Basic Resource

**HCL (Terraform)**
```hcl
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"

  tags = {
    Name = "web-server"
  }
}
```

**YAML (ytofu)**
```yaml
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      tags:
        Name: web-server
```

### Multiple Resources

**HCL (Terraform)**
```hcl
resource "aws_subnet" "public_a" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-west-2a"
}

resource "aws_subnet" "public_b" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-west-2b"
}
```

**YAML (ytofu)**
```yaml
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
```

### Lists and Maps

**HCL (Terraform)**
```hcl
resource "aws_security_group" "web" {
  name   = "web-sg"
  vpc_id = aws_vpc.main.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

**YAML (ytofu)**
```yaml
resource:
  aws_security_group:
    web:
      name: web-sg
      vpc_id: ${aws_vpc.main.id}

      ingress:
        - from_port: 80
          to_port: 80
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0

        - from_port: 443
          to_port: 443
          protocol: tcp
          cidr_blocks:
            - 0.0.0.0/0
```

### Data Sources

**HCL (Terraform)**
```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-*-amd64-server-*"]
  }
}
```

**YAML (ytofu)**
```yaml
data:
  aws_ami:
    ubuntu:
      most_recent: true
      owners:
        - "099720109477"
      filter:
        - name: name
          values:
            - ubuntu/images/hvm-ssd/ubuntu-*-amd64-server-*
```

### Provider Configuration

**HCL (Terraform)**
```hcl
provider "aws" {
  region = "us-west-2"

  default_tags {
    tags = {
      Environment = "production"
      ManagedBy   = "ytofu"
    }
  }
}
```

**YAML (ytofu)**
```yaml
provider:
  aws:
    region: us-west-2
    default_tags:
      tags:
        Environment: production
        ManagedBy: ytofu
```

## Key Differences

| Aspect | HCL | YAML |
|--------|-----|------|
| Block syntax | `resource "type" "name" { }` | Nested keys |
| Quotes | Optional for strings | Optional (usually) |
| Lists | `[a, b, c]` | `- item` format |
| Comments | `#` or `//` or `/* */` | `#` only |
| Multi-line strings | `<<EOF ... EOF` | `\|` or `>` |
| File extension | `.tf` | `.yaml` or `.yml` |

## Multi-line Strings

**HCL (Terraform)**
```hcl
resource "aws_iam_policy" "example" {
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "s3:GetObject",
    "Resource": "*"
  }]
}
EOF
}
```

**YAML (ytofu)**
```yaml
resource:
  aws_iam_policy:
    example:
      policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "*"
          }]
        }
```

## What YAML Cannot Do

YAML in ytofu intentionally omits:

| HCL Feature | Status in ytofu |
|-------------|-----------------|
| `variable` blocks | Not supported |
| `locals` blocks | Not supported |
| `for_each` | Not supported |
| `count` | Not supported |
| `for` expressions | Not supported |
| Functions | Not supported |
| `dynamic` blocks | Not supported |
| Conditionals | Not supported |

This is by design. See [Configuration as Data](configuration-as-data.md) for the rationale.

## Conversion Tips

When converting HCL to YAML:

1. **Replace blocks with nested keys**
   - `resource "aws_instance" "web"` becomes `resource: aws_instance: web:`

2. **Convert lists to YAML format**
   - `["a", "b"]` becomes `- a` and `- b` on separate lines

3. **Remove variables** - Replace with concrete values

4. **Remove loops** - Create explicit resources

5. **Remove functions** - Use pre-calculated values

## Benefits of YAML

- **Familiar syntax** - Used in Kubernetes, Ansible, GitHub Actions
- **Tool ecosystem** - Linters, validators, generators
- **Language-agnostic** - Parse and generate from any language
- **Human-readable** - Clean, minimal syntax

## Related

- [Configuration as Data](configuration-as-data.md)
- [Resource Lifecycle](resource-lifecycle.md)
- [Getting Started](../getting-started.md)
