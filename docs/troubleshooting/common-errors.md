# Common Errors

Solutions to frequently encountered error messages.

## Provider Errors

### Error: No valid credential sources found

```
Error: No valid credential sources found for AWS Provider.
```

**Cause:** AWS credentials not configured.

**Solution:**
```bash
# Option 1: Environment variables
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"

# Option 2: AWS CLI configuration
aws configure

# Option 3: IAM role (EC2, ECS, Lambda)
# Credentials are automatic
```

### Error: UnauthorizedAccess

```
Error: error creating EC2 Instance: UnauthorizedOperation
```

**Cause:** IAM permissions insufficient.

**Solution:** Ensure your IAM user/role has the required permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "elasticloadbalancing:*",
        "ecs:*"
      ],
      "Resource": "*"
    }
  ]
}
```

## State Errors

### Error: state lock

```
Error: Error acquiring the state lock
Lock Info:
  ID:        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  Path:      s3://bucket/terraform.tfstate
  Operation: OperationTypeApply
```

**Cause:** Another operation is in progress or a previous operation didn't complete cleanly.

**Solution:**

```bash
# Wait for the other operation to complete, or if stuck:
ytofu force-unlock xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

### Error: state out of sync

```
Error: Resource "aws_instance.web" not found in state
```

**Cause:** Resource was deleted outside of ytofu.

**Solution:**
```bash
# Refresh state from AWS
ytofu refresh

# Or import the resource
ytofu import aws_instance.web i-1234567890abcdef0
```

## Resource Errors

### Error: Resource already exists

```
Error: error creating VPC: VpcLimitExceeded
```

**Cause:** AWS service limit reached or resource already exists.

**Solution:**
1. Check existing resources in AWS Console
2. Request limit increase if needed
3. Import existing resource into state

### Error: InvalidParameterValue

```
Error: error creating EC2 Instance: InvalidParameterValue:
Invalid value 'ami-invalid' for AMI ID
```

**Cause:** Invalid or unavailable AMI ID.

**Solution:**
```yaml
# Use data source to find valid AMI
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

resource:
  aws_instance:
    web:
      ami: ${data.aws_ami.ubuntu.id}
```

### Error: DependencyViolation

```
Error: error deleting VPC: DependencyViolation:
The vpc 'vpc-xxx' has dependencies and cannot be deleted.
```

**Cause:** VPC has attached resources that must be deleted first.

**Solution:**
```bash
# Delete resources in correct order
ytofu destroy -target=aws_instance.web
ytofu destroy -target=aws_subnet.public
ytofu destroy -target=aws_internet_gateway.main
ytofu destroy -target=aws_vpc.main
```

## Networking Errors

### Error: No internet access from private subnet

**Symptoms:** Private instances can't reach the internet.

**Causes and Solutions:**

| Cause | Solution |
|-------|----------|
| No NAT Gateway | Create NAT Gateway in public subnet |
| Missing route | Add 0.0.0.0/0 route to NAT Gateway |
| Wrong route table | Associate correct route table with subnet |
| Security group | Allow outbound traffic in security group |

### Error: Cannot connect to instance

**Symptoms:** SSH/HTTP connections timeout.

**Checklist:**

```yaml
# 1. Instance in public subnet?
aws_subnet:
  public:
    map_public_ip_on_launch: true  # Required

# 2. Security group allows traffic?
aws_security_group:
  web:
    ingress:
      - from_port: 22
        to_port: 22
        protocol: tcp
        cidr_blocks:
          - 0.0.0.0/0

# 3. Route table has IGW route?
aws_route_table:
  public:
    route:
      - cidr_block: 0.0.0.0/0
        gateway_id: ${aws_internet_gateway.main.id}
```

### Error: Target group has no healthy targets

**Symptoms:** ALB returns 502/503 errors.

**Causes and Solutions:**

| Cause | Solution |
|-------|----------|
| Instance not running | Start the instance |
| Wrong port | Match target group port with app port |
| Health check failing | Fix health check path or app |
| Security group | Allow ALB to reach instance |

## YAML Syntax Errors

### Error: Invalid YAML

```
Error: Argument or block definition required
```

**Cause:** YAML indentation or syntax error.

**Solution:** Check for:
- Consistent indentation (2 spaces recommended)
- Missing colons after keys
- Incorrect list syntax

```yaml
# WRONG - missing colon
resource
  aws_instance:

# CORRECT
resource:
  aws_instance:

# WRONG - incorrect list
ingress:
  from_port: 80

# CORRECT
ingress:
  - from_port: 80
```

### Error: Reference to undeclared resource

```
Error: Reference to undeclared resource
  on main.yaml line 10:
  vpc_id: ${aws_vpc.main.id}
```

**Cause:** Resource name typo or resource not defined.

**Solution:**
1. Check resource name matches exactly
2. Ensure resource is defined
3. Check for typos in reference

## Timeout Errors

### Error: timeout while waiting for state

```
Error: timeout while waiting for state to become 'available'
```

**Cause:** AWS operation taking longer than expected.

**Solution:**
```yaml
resource:
  aws_db_instance:
    main:
      # ... configuration ...
      timeouts:
        create: 60m
        update: 60m
        delete: 60m
```

Common resources with long creation times:
- RDS instances (10-20 minutes)
- EKS clusters (10-15 minutes)
- NAT Gateways (3-5 minutes)
- CloudFront distributions (15-30 minutes)

## Getting More Help

If your error isn't listed:

1. **Search the error message** online
2. **Check AWS documentation** for the specific service
3. **Enable debug logging**: `TF_LOG=DEBUG ytofu plan`
4. **Open an issue** with reproduction steps

## Related

- [Troubleshooting Overview](index.md)
- [Resource Lifecycle](../concepts/resource-lifecycle.md)
- [Getting Started](../getting-started.md)
