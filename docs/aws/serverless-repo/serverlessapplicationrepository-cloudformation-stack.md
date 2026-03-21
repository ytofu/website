# Serverlessapplicationrepository Cloudformation Stack

Manage Serverlessapplicationrepository Cloudformation Stack resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_serverlessapplicationrepository_cloudformation_stack:
    postgres-rotator:
      name: postgres-rotator
      application_id: "arn:aws:serverlessrepo:us-east-1:297356227824:applications/SecretsManagerRDSPostgreSQLRotationSingleUser"
      capabilities:
        - CAPABILITY_IAM
        - CAPABILITY_RESOURCE_POLICY
      parameters:
        functionName: func-postgres-rotator
        endpoint: "secretsmanager.${data.aws_region.current.region}.${data.aws_partition.current.dns_suffix}"

data:
  aws_partition:
    current:

data:
  aws_region:
    current:
```
