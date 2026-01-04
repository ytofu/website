# Getting Started

This guide will help you get up and running with ytofu.

## Installation

### From Binary

Download the latest release from GitHub:

```bash
# Linux/macOS
curl -LO https://github.com/ytofu/ytofu/releases/latest/download/ytofu_linux_amd64.tar.gz
tar -xzf ytofu_linux_amd64.tar.gz
sudo mv ytofu /usr/local/bin/
```

### From Source

```bash
git clone https://github.com/ytofu/ytofu.git
cd ytofu
go build -o ytofu ./cmd/ytofu
```

## Your First Configuration

Create a file named `main.yaml`:

```yaml
terraform:
  required_providers:
    local:
      source: hashicorp/local
      version: "~> 2.0"

resource:
  local_file:
    hello:
      filename: hello.txt
      content: "Hello from ytofu!"
```

## Initialize and Apply

```bash
# Initialize the working directory
ytofu init

# Preview the changes
ytofu plan

# Apply the configuration
ytofu apply
```

## Next Steps

- Explore more examples in the documentation
- Learn about the YAML schema for Terraform resources
- Join the community on GitHub
