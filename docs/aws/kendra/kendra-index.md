# Kendra Index

Manage Kendra Index resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      description: example
      edition: DEVELOPER_EDITION
      role_arn: ${aws_iam_role.this.arn}
      tags: 
```

## With capacity units

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      edition: DEVELOPER_EDITION
      role_arn: ${aws_iam_role.this.arn}
      capacity_units:
        query_capacity_units: 2
        storage_capacity_units: 2
```

## With server side encryption configuration

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      role_arn: ${aws_iam_role.this.arn}
      server_side_encryption_configuration:
        kms_key_id: ${data.aws_kms_key.this.arn}
```

## With user group resolution configuration

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      role_arn: ${aws_iam_role.this.arn}
      user_group_resolution_configuration:
        user_group_resolution_mode: AWS_SSO
```

## With Document Metadata Configuration Updates

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      role_arn: ${aws_iam_role.this.arn}
      document_metadata_configuration_updates:
        name: _authors
        type: STRING_LIST_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: false
        relevance:
          importance: 1
      document_metadata_configuration_updates:
        name: _category
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _created_at
        type: DATE_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          freshness: false
          importance: 1
          duration: 25920000s
          rank_order: ASCENDING
      document_metadata_configuration_updates:
        name: _data_source_id
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _document_title
        type: STRING_VALUE
        search:
          displayable: true
          facetable: false
          searchable: true
          sortable: true
        relevance:
          importance: 2
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _excerpt_page_number
        type: LONG_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: false
        relevance:
          importance: 2
          rank_order: ASCENDING
      document_metadata_configuration_updates:
        name: _faq_id
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _file_type
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _language_code
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _last_updated_at
        type: DATE_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          freshness: false
          importance: 1
          duration: 25920000s
          rank_order: ASCENDING
      document_metadata_configuration_updates:
        name: _source_uri
        type: STRING_VALUE
        search:
          displayable: true
          facetable: false
          searchable: false
          sortable: false
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _tenant_id
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _version
        type: STRING_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          values_importance_map: {}
      document_metadata_configuration_updates:
        name: _view_count
        type: LONG_VALUE
        search:
          displayable: false
          facetable: false
          searchable: false
          sortable: true
        relevance:
          importance: 1
          rank_order: ASCENDING
```

## With JSON token type configuration

```yaml
resource:
  aws_kendra_index:
    example:
      name: example
      role_arn: ${aws_iam_role.this.arn}
      user_token_configurations:
        json_token_type_configuration:
          group_attribute_field: groups
          user_name_attribute_field: username
```
