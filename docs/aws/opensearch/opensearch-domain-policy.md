# Resource: aws_opensearch_domain_policy

Allows setting policy to an OpenSearch domain while referencing domain attributes (e.g., ARN).

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: tf-test
      engine_version: OpenSearch_1.1

  aws_opensearch_domain_policy:
    main:
      domain_name: ${aws_opensearch_domain.example.domain_name}
      access_policies: ${data.aws_iam_policy_document.main.json}

data:
  aws_iam_policy_document:
    main:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "es:*"
        resources: 
          - "${aws_opensearch_domain.example.arn}/*"
        condition:
          test: IpAddress
          values: 
            - 127.0.0.1/32```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `access_policies` - (Optional) IAM policy document specifying the access policies for the domain
* `domain_name` - (Required) Name of the domain.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `update` - (Default `180m`)
* `delete` - (Default `90m`)

## Import

```bash
ytofu import aws_opensearch_domain_policy.example esd-policy-tf-test
```
