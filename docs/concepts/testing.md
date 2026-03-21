# Testing Framework

ytofu includes a built-in testing framework for validating your infrastructure configurations. Write tests to ensure your modules work correctly before deploying to production.

## Overview

The testing framework allows you to:
- Validate resource configurations
- Test module behavior
- Assert expected outputs
- Use mock providers for isolated testing

## Running Tests

Execute tests with the `test` command:

```bash
ytofu test
```

Test files use the `.tftest.hcl` extension and are discovered automatically.

## Test File Structure

Create test files alongside your configuration:

```
project/
├── main.tf
├── variables.tf
├── outputs.tf
└── tests/
    └── main.tftest.hcl
```

## Basic Test Example

**main.tftest.hcl**
```hcl
run "verify_instance_type" {
  command = plan

  assert {
    condition     = aws_instance.web.instance_type == "t3.micro"
    error_message = "Instance type must be t3.micro"
  }
}
```

## Test Commands

Tests can use different commands:

### Plan Tests

Validate configuration without creating resources:

```hcl
run "validate_configuration" {
  command = plan

  assert {
    condition     = aws_instance.web.ami != ""
    error_message = "AMI must be specified"
  }
}
```

### Apply Tests

Create real resources and validate them:

```hcl
run "create_and_verify" {
  command = apply

  assert {
    condition     = aws_instance.web.id != ""
    error_message = "Instance should be created"
  }
}
```

## Variables in Tests

Override variables for specific test scenarios:

```hcl
run "test_production_config" {
  command = plan

  variables {
    environment   = "production"
    instance_type = "t3.large"
  }

  assert {
    condition     = aws_instance.web.instance_type == "t3.large"
    error_message = "Production should use t3.large"
  }
}
```

## Mock Providers

Use mock providers to test without real cloud resources:

```hcl
mock_provider "aws" {
  mock_resource "aws_instance" {
    defaults = {
      id               = "i-mock12345"
      public_ip        = "1.2.3.4"
      private_ip       = "10.0.0.1"
      availability_zone = "us-west-2a"
    }
  }

  mock_data "aws_ami" {
    defaults = {
      id   = "ami-mock12345"
      name = "mock-ami"
    }
  }
}

run "test_with_mock" {
  providers = {
    aws = mock_provider.aws
  }

  command = apply

  assert {
    condition     = aws_instance.web.id == "i-mock12345"
    error_message = "Should use mock instance ID"
  }
}
```

## Testing Modules

Test modules by referencing them:

```hcl
run "test_vpc_module" {
  module {
    source = "./modules/vpc"
  }

  variables {
    cidr_block = "10.0.0.0/16"
    name       = "test-vpc"
  }

  assert {
    condition     = output.vpc_id != ""
    error_message = "VPC should be created"
  }
}
```

## Multiple Test Runs

Chain multiple test runs together:

```hcl
run "setup" {
  command = apply

  variables {
    create_vpc = true
  }
}

run "verify_vpc" {
  command = plan

  assert {
    condition     = aws_vpc.main.id != ""
    error_message = "VPC should exist from setup"
  }
}

run "add_subnet" {
  command = apply

  variables {
    create_vpc    = true
    create_subnet = true
  }

  assert {
    condition     = aws_subnet.main.vpc_id == aws_vpc.main.id
    error_message = "Subnet should be in the VPC"
  }
}
```

## Assertions

### Condition Assertions

Check boolean conditions:

```hcl
assert {
  condition     = length(aws_instance.web) > 0
  error_message = "At least one instance should be created"
}
```

### Output Assertions

Validate output values:

```hcl
assert {
  condition     = output.instance_count == 3
  error_message = "Should create exactly 3 instances"
}
```

### Complex Conditions

Use expressions for complex validations:

```hcl
assert {
  condition = alltrue([
    aws_instance.web.instance_type == "t3.micro",
    aws_instance.web.monitoring == true,
    length(aws_instance.web.tags) > 0
  ])
  error_message = "Instance configuration is invalid"
}
```

## Test Cleanup

By default, resources created during tests are destroyed after the test run. Control this behavior:

```hcl
run "persistent_test" {
  command = apply

  # Keep resources after test (useful for debugging)
  # destroy = false
}
```

## Test Output

View detailed test output:

```bash
# Verbose output
ytofu test -verbose

# JSON output for CI/CD
ytofu test -json
```

Example output:
```
tests/main.tftest.hcl... pass
  run "verify_instance_type"... pass
  run "test_production_config"... pass

Success! 2 passed, 0 failed.
```

## Organizing Tests

### By Feature

```
tests/
├── networking.tftest.hcl
├── compute.tftest.hcl
└── security.tftest.hcl
```

### By Environment

```
tests/
├── development.tftest.hcl
├── staging.tftest.hcl
└── production.tftest.hcl
```

## Best Practices

1. **Test early and often** - Run tests in CI/CD pipelines

2. **Use mock providers** - Avoid creating real resources for unit tests

3. **Test edge cases** - Validate behavior with unusual inputs

4. **Keep tests focused** - Each test should verify one thing

5. **Use descriptive names** - Make it clear what each test validates

6. **Clean up resources** - Ensure test resources are destroyed

## CI/CD Integration

Example GitHub Actions workflow:

```yaml
name: Test Infrastructure
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup ytofu
        run: |
          curl -LO https://github.com/ytofu/ytofu/releases/latest/download/ytofu_linux_amd64.tar.gz
          tar -xzf ytofu_linux_amd64.tar.gz
          sudo mv ytofu /usr/local/bin/

      - name: Run Tests
        run: ytofu test -json > test-results.json

      - name: Upload Results
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: test-results.json
```

## Related

- [Resource Lifecycle](resource-lifecycle.md)
- [Configuration as Data](configuration-as-data.md)
