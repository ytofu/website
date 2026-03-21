# Resource: aws_bedrockagentcore_workload_identity

Manages an AWS Bedrock AgentCore Workload Identity. Workload Identity provides OAuth2-based authentication and authorization for AI agents to access external resources securely.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_workload_identity:
    example:
      name: example-workload-identity
      allowed_resource_oauth2_return_urls:
        - "https://example.com/callback"
```

## Workload Identity with Multiple Return URLs

```yaml
resource:
  aws_bedrockagentcore_workload_identity:
    example:
      name: example-workload-identity
      allowed_resource_oauth2_return_urls:
        - "https://app.example.com/oauth/callback"
        - "https://api.example.com/auth/return"
        - "https://example.com/callback"
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the workload identity. Must be 3-255 characters and contain only alphanumeric characters, hyphens, periods, and underscores.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allowed_resource_oauth2_return_urls` - (Optional) Set of allowed OAuth2 return URLs for resources associated with this workload identity. These URLs are used as valid redirect targets during OAuth2 authentication flows.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `workload_identity_arn` - ARN of the Workload Identity.

## Import

```bash
ytofu import aws_bedrockagentcore_workload_identity.example example-workload-identity
```
