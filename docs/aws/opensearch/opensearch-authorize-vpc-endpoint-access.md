# Resource: aws_opensearch_authorize_vpc_endpoint_access

ytofu resource for managing an AWS OpenSearch Authorize Vpc Endpoint Access.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_opensearch_authorize_vpc_endpoint_access:
    test:
      domain_name: ${aws_opensearch_domain.test.domain_name}
      account: ${data.aws_caller_identity.current.account_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `account` - (Required) AWS account ID to grant access to.
* `domain_name` - (Required) Name of OpenSearch Service domain to provide access to.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `authorized_principal` - Information about the Amazon Web Services account or service that was provided access to the domain. See [authorized principal](#authorized_principal) attribute for further details.

### authorized_principal

* `principal` - IAM principal that is allowed to access to the domain.
* `principal_type` - Type of principal.

## Import

```bash
ytofu import aws_opensearch_authorize_vpc_endpoint_access.example authorize_vpc_endpoint_access-id-12345678,123456789012
```
