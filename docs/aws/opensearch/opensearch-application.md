# Opensearch Application

Manage Opensearch Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_application:
    example:
      name: my-opensearch-app
```

## Application with Configuration

```yaml
resource:
  aws_opensearch_application:
    example:
      name: my-opensearch-app
      app_config:
        key: opensearchDashboards.dashboardAdmin.users
        value: admin-user
      app_config:
        key: opensearchDashboards.dashboardAdmin.groups
        value: admin-group
      tags:
        Environment: production
        Team: data-platform
```

## Application with Data Sources

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example-domain
      engine_version: OpenSearch_2.3
      cluster_config:
        instance_type: t3.small.search
      ebs_options:
        ebs_enabled: true
        volume_size: 20

resource:
  aws_opensearch_application:
    example:
      name: my-opensearch-app
      data_source:
        data_source_arn: ${aws_opensearch_domain.example.arn}
        data_source_description: Primary OpenSearch domain for analytics
      tags:
        Environment: production
```

## Application with IAM Identity Center Integration

```yaml
data:
  aws_ssoadmin_instances:
    example:

data:
  aws_caller_identity:
    current:

data:
  aws_region:
    current:

resource:
  aws_iam_policy:
    opensearch_identity_center:
      name: opensearch-identity-center-policy
      description: Policy for OpenSearch Application Identity Center integration
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid": "IdentityStoreOpenSearchDomainConnectivity" "Effect": "Allow" "Action": [ "identitystore:DescribeUser", "identitystore:ListGroupMembershipsForMember", "identitystore:DescribeGroup" ] "Resource": "*" "Condition": { "ForAnyValue:StringEquals" = { "aws:CalledViaLast" = "es.amazonaws.com" } } }, { "Sid": "OpenSearchDomain" "Effect": "Allow" "Action": [ "es:ESHttp*" ] "Resource": "*" }, { "Sid": "OpenSearchServerless" "Effect": "Allow" "Action": [ "aoss:APIAccessAll" ] "Resource": "*" } ] }'

resource:
  aws_iam_role:
    opensearch_application:
      name: opensearch-application-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Principal": { "Service": "application.opensearchservice.amazonaws.com" } "Action": "sts:AssumeRole" }, { "Effect": "Allow" "Principal": { "Service": "application.opensearchservice.amazonaws.com" } "Action": "sts:SetContext" "Condition": { "ForAllValues:ArnEquals" = { "sts:RequestContextProviders" = "arn:aws:iam::${data.aws_caller_identity.current.account_id}:oidc-provider/portal.sso.${data.aws_region.current.id}.amazonaws.com/apl/*" } } } ] }'

resource:
  aws_iam_role_policy_attachment:
    opensearch_identity_center:
      role: ${aws_iam_role.opensearch_application.name}
      policy_arn: ${aws_iam_policy.opensearch_identity_center.arn}

resource:
  aws_opensearch_application:
    example:
      name: my-opensearch-app
      iam_identity_center_options:
        enabled: true
        iam_identity_center_instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
        iam_role_for_identity_center_application_arn: ${aws_iam_role.opensearch_application.arn}
      tags:
        Environment: production
```
