# Transfer Server

Manage Transfer Server resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_server:
    example:
      tags:
        Name: Example
```

## Security Policy Name

```yaml
resource:
  aws_transfer_server:
    example:
      security_policy_name: TransferSecurityPolicy-2020-06
```

## VPC Endpoint

```yaml
resource:
  aws_transfer_server:
    example:
      endpoint_type: VPC
      endpoint_details:
        address_allocation_ids: 
          - ${aws_eip.example.id}
        subnet_ids: 
          - ${aws_subnet.example.id}
        vpc_id: ${aws_vpc.example.id}
```

## AWS Directory authentication

```yaml
resource:
  aws_transfer_server:
    example:
      identity_provider_type: AWS_DIRECTORY_SERVICE
      directory_id: ${aws_directory_service_directory.example.id}
```

## AWS Lambda authentication

```yaml
resource:
  aws_transfer_server:
    example:
      identity_provider_type: AWS_LAMBDA
      function: ${aws_lambda_identity_provider.example.arn}
```

## Protocols

```yaml
resource:
  aws_transfer_server:
    example:
      endpoint_type: VPC
      endpoint_details:
        subnet_ids: 
          - ${aws_subnet.example.id}
        vpc_id: ${aws_vpc.example.id}
      protocols: 
        - FTP
        - FTPS
      certificate: ${aws_acm_certificate.example.arn}
      identity_provider_type: API_GATEWAY
      url: "${aws_api_gateway_deployment.example.invoke_url}${aws_api_gateway_resource.example.path}"
```

## Using Structured Logging Destinations

```yaml
resource:
  aws_cloudwatch_log_group:
    transfer:
      name_prefix: transfer_test_

data:
  aws_iam_policy_document:
    transfer_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - transfer.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    iam_for_transfer:
      name_prefix: iam_for_transfer_
      assume_role_policy: ${data.aws_iam_policy_document.transfer_assume_role.json}
      managed_policy_arns: 
        - "arn:aws:iam::aws:policy/service-role/AWSTransferLoggingAccess"

resource:
  aws_transfer_server:
    transfer:
      endpoint_type: PUBLIC
      logging_role: ${aws_iam_role.iam_for_transfer.arn}
      protocols: 
        - SFTP
      structured_log_destinations:
        - "${aws_cloudwatch_log_group.transfer.arn}:*"
```
