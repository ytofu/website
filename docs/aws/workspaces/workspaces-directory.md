# Workspaces Directory

Manage Workspaces Directory resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspaces_directory:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      subnet_ids:
        - ${aws_subnet.example_c.id}
        - ${aws_subnet.example_d.id}
      tags:
        Example: true
      certificate_based_auth_properties:
        certificate_authority_arn: "arn:aws:acm-pca:us-east-1:123456789012:certificate-authority/12345678-1234-1234-1234-123456789012"
        status: ENABLED
      saml_properties:
        user_access_url: "https://sso.example.com/"
        status: ENABLED
      self_service_permissions:
        change_compute_type: true
        increase_volume_size: true
        rebuild_workspace: true
        restart_workspace: true
        switch_running_mode: true
      workspace_access_properties:
        device_type_android: ALLOW
        device_type_chromeos: ALLOW
        device_type_ios: ALLOW
        device_type_linux: DENY
        device_type_osx: ALLOW
        device_type_web: DENY
        device_type_windows: DENY
        device_type_zeroclient: DENY
      workspace_creation_properties:
        custom_security_group_id: ${aws_security_group.example.id}
        default_ou: OU=AWS,DC=Workgroup,DC=Example,DC=com
        enable_internet_access: true
        enable_maintenance_mode: true
        user_enabled_as_local_administrator: true
      depends_on:
        - ${aws_iam_role_policy_attachment.workspaces_default_service_access}
        - ${aws_iam_role_policy_attachment.workspaces_default_self_service_access}

resource:
  aws_directory_service_directory:
    example:
      name: corp.example.com
      password: "#S1ncerely"
      size: Small
      vpc_settings:
        vpc_id: ${aws_vpc.example.id}
        subnet_ids:
          - ${aws_subnet.example_a.id}
          - ${aws_subnet.example_b.id}

data:
  aws_iam_policy_document:
    workspaces:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - workspaces.amazonaws.com

resource:
  aws_iam_role:
    workspaces_default:
      name: workspaces_DefaultRole
      assume_role_policy: ${data.aws_iam_policy_document.workspaces.json}

resource:
  aws_iam_role_policy_attachment:
    workspaces_default_service_access:
      role: ${aws_iam_role.workspaces_default.name}
      policy_arn: "arn:aws:iam::aws:policy/AmazonWorkSpacesServiceAccess"

resource:
  aws_iam_role_policy_attachment:
    workspaces_default_self_service_access:
      role: ${aws_iam_role.workspaces_default.name}
      policy_arn: "arn:aws:iam::aws:policy/AmazonWorkSpacesSelfServiceAccess"

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example_a:
      vpc_id: ${aws_vpc.example.id}
      availability_zone: us-east-1a
      cidr_block: 10.0.0.0/24

resource:
  aws_subnet:
    example_b:
      vpc_id: ${aws_vpc.example.id}
      availability_zone: us-east-1b
      cidr_block: 10.0.1.0/24

resource:
  aws_subnet:
    example_c:
      vpc_id: ${aws_vpc.example.id}
      availability_zone: us-east-1c
      cidr_block: 10.0.2.0/24

resource:
  aws_subnet:
    example_d:
      vpc_id: ${aws_vpc.example.id}
      availability_zone: us-east-1d
      cidr_block: 10.0.3.0/24
```

## WorkSpaces Pools

```yaml
resource:
  aws_workspaces_directory:
    example:
      subnet_ids:
        - ${aws_subnet.example_c.id}
        - ${aws_subnet.example_d.id}
      workspace_type: POOLS
      workspace_directory_name: Pool directory
      workspace_directory_description: WorkSpaces Pools directory
      user_identity_type: CUSTOMER_MANAGED
      active_directory_config:
        domain_name: example.internal
        service_account_secret_arn: ${aws_secretsmanager_secret.example.arn}
      workspace_access_properties:
        device_type_android: ALLOW
        device_type_chromeos: ALLOW
        device_type_ios: ALLOW
        device_type_linux: DENY
        device_type_osx: ALLOW
        device_type_web: DENY
        device_type_windows: DENY
        device_type_zeroclient: DENY
      workspace_creation_properties:
        custom_security_group_id: ${aws_security_group.example.id}
        default_ou: OU=AWS,DC=Workgroup,DC=Example,DC=com
        enable_internet_access: true
      saml_properties:
        relay_state_parameter_name: RelayState
        user_access_url: "https://sso.example.com/"
        status: ENABLED
```

## IP Groups

```yaml
resource:
  aws_workspaces_directory:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      ip_group_ids:
        - ${aws_workspaces_ip_group.example.id}

resource:
  aws_workspaces_ip_group:
    example:
      name: example
```
