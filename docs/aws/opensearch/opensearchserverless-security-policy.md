# Resource: aws_opensearchserverless_security_policy

ytofu resource for managing an AWS OpenSearch Serverless Security Policy. See AWS documentation for [encryption policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/serverless-encryption.html#serverless-encryption-policies) and [network policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/serverless-network.html#serverless-network-policies).

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: encryption
      description: encryption security policy for example-collection
      policy: '{ "Rules": [ { "Resource": [ "collection/example-collection" ], "ResourceType": "collection" } ], "AWSOwnedKey": true }'
```

## Network Security Policy

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: network
      description: Public access
      policy: 'example-json-policy'
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the policy.
* `policy` - (Required) JSON policy document to use as the content for the new policy
* `type` - (Required) Type of security policy. One of `encryption` or `network`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the policy. Typically used to store information about the permissions defined in the policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `policy_version` - Version of the policy.

## Import

```bash
ytofu import aws_opensearchserverless_security_policy.example example/encryption
```
