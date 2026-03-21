# Route53domains Domain

Manage Route53domains Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53domains_domain:
    example:
      domain_name: example.com
      auto_renew: false
      admin_contact:
        address_line_1: 101 Main Street
        city: San Francisco
        contact_type: COMPANY
        country_code: US
        email: terraform-acctest@example.com
        fax: +1.4155551234
        first_name: Terraform
        last_name: Team
        organization_name: HashiCorp
        phone_number: +1.4155551234
        state: CA
        zip_code: 94105
      registrant_contact:
        address_line_1: 101 Main Street
        city: San Francisco
        contact_type: COMPANY
        country_code: US
        email: terraform-acctest@example.com
        fax: +1.4155551234
        first_name: Terraform
        last_name: Team
        organization_name: HashiCorp
        phone_number: +1.4155551234
        state: CA
        zip_code: 94105
      tech_contact:
        address_line_1: 101 Main Street
        city: San Francisco
        contact_type: COMPANY
        country_code: US
        email: terraform-acctest@example.com
        fax: +1.4155551234
        first_name: Terraform
        last_name: Team
        organization_name: HashiCorp
        phone_number: +1.4155551234
        state: CA
        zip_code: 94105
      tags:
        Environment: test
```
