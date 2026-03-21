# Resource: aws_cloudsearch_domain_service_access_policy

Provides an CloudSearch domain service access policy resource.

## Basic Example

```yaml
resource:
  aws_cloudsearch_domain:
    example:
      name: example-domain

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: search_only
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions:
          - "cloudsearch:search"
          - "cloudsearch:document"
        condition:
          test: IpAddress
          values: 
            - 192.0.2.0/32

resource:
  aws_cloudsearch_domain_service_access_policy:
    example:
      domain_name: ${aws_cloudsearch_domain.example.id}
      access_policy: ${data.aws_iam_policy_document.example.json}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `access_policy` - (Required) The access rules you want to configure. These rules replace any existing rules. See the [AWS documentation](https://docs.aws.amazon.com/cloudsearch/latest/developerguide/configuring-access.html) for details.
* `domain_name` - (Required) The CloudSearch domain name the policy applies to.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `update` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_cloudsearch_domain_service_access_policy.example example-domain
```
