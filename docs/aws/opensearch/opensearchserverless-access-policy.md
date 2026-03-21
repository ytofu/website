# Resource: aws_opensearchserverless_access_policy

ytofu resource for managing an AWS OpenSearch Serverless Access Policy. See AWS documentation for [data access policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/serverless-data-access.html) and [supported data access policy permissions](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/serverless-data-access.html#serverless-data-supported-permissions).

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_opensearchserverless_access_policy:
    example:
      name: example
      type: data
      description: read and write permissions
      policy: 'example-json-policy'
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the policy.
* `policy` - (Required) JSON policy document to use as the content for the new policy
* `type` - (Required) Type of access policy. Must be `data`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the policy. Typically used to store information about the permissions defined in the policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `policy_version` - Version of the policy.

## Import

```bash
ytofu import aws_opensearchserverless_access_policy.example example/data
```
