# Organizational Unit

Create organizational units using ytofu YAML.

## Basic OU

```yaml
resource:
  aws_organizations_organizational_unit:
    production:
      name: Production
      parent_id: ${aws_organizations_organization.org.roots[0].id}
```

## Nested OUs

```yaml
resource:
  aws_organizations_organizational_unit:
    workloads:
      name: Workloads
      parent_id: ${aws_organizations_organization.org.roots[0].id}

  aws_organizations_organizational_unit:
    production:
      name: Production
      parent_id: ${aws_organizations_organizational_unit.workloads.id}

  aws_organizations_organizational_unit:
    staging:
      name: Staging
      parent_id: ${aws_organizations_organizational_unit.workloads.id}
```
