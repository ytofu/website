# Glue Connection

Manage Glue Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_connection:
    example:
      name: example
      connection_properties:
        JDBC_CONNECTION_URL: "jdbc:mysql://example.com/exampledatabase"
        PASSWORD: examplepassword
        USERNAME: exampleusername
```

## Non-VPC Connection with secret manager reference

```yaml
data:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_glue_connection:
    example:
      name: example
      connection_properties:
        JDBC_CONNECTION_URL: "jdbc:mysql://example.com/exampledatabase"
        SECRET_ID: ${data.aws_secretsmanager_secret.example.name}
```

## VPC Connection

```yaml
resource:
  aws_glue_connection:
    example:
      name: example
      connection_properties:
        JDBC_CONNECTION_URL: "jdbc:mysql://${aws_rds_cluster.example.endpoint}/exampledatabase"
        PASSWORD: examplepassword
        USERNAME: exampleusername
      physical_connection_requirements:
        availability_zone: ${aws_subnet.example.availability_zone}
        security_group_id_list: 
          - ${aws_security_group.example.id}
        subnet_id: ${aws_subnet.example.id}
```

## Connection using a custom connector

```yaml
data:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_glue_connection:
    example1:
      name: example1
      connection_type: CUSTOM
      connection_properties:
        CONNECTOR_CLASS_NAME: net.snowflake.client.jdbc.SnowflakeDriver
        CONNECTION_TYPE: Jdbc
        CONNECTOR_URL: "s3://example/snowflake-jdbc.jar" # S3 path to the snowflake jdbc jar
        JDBC_CONNECTION_URL: "[[\"default=jdbc:snowflake://example.com/?user=$${user}&password=$${password}\"],\",\"]"
      match_criteria: 
        - template-connection

resource:
  aws_glue_connection:
    example2:
      name: example2
      connection_type: CUSTOM
      connection_properties:
        CONNECTOR_CLASS_NAME: net.snowflake.client.jdbc.SnowflakeDriver
        CONNECTION_TYPE: Jdbc
        CONNECTOR_URL: "s3://example/snowflake-jdbc.jar"
        JDBC_CONNECTION_URL: "jdbc:snowflake://example.com/?user=$${user}&password=$${password}"
        SECRET_ID: ${data.aws_secretsmanager_secret.example.name}
      match_criteria: 
        - Connection
        - ${aws_glue_connection.example1.name}
```

## Azure Cosmos Connection

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: '{ "username": "exampleusername" "password": "examplepassword" }'

resource:
  aws_glue_connection:
    example:
      name: example
      connection_type: AZURECOSMOS
      connection_properties:
        SparkProperties: '{ "secretId": aws_secretsmanager_secret.example.name "spark.cosmos.accountEndpoint" = "https://exampledbaccount.documents.azure.com:443/" }'
```

## Azure SQL Connection

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: '{ "username": "exampleusername" "password": "examplepassword" }'

resource:
  aws_glue_connection:
    example:
      name: example
      connection_type: AZURECOSMOS
      connection_properties:
        SparkProperties: '{ "secretId": aws_secretsmanager_secret.example.name "url": "jdbc:sqlserver:exampledbserver.database.windows.net:1433;"database": exampledatabase" }'
```

## Google BigQuery Connection

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: '{ "credentials": base64encode(<<-EOT { "type": "service_account", "project_id": "example-project", "private_key_id": "example-key", "private_key": "-----BEGIN RSA PRIVATE KEY-----\nREDACTED\n-----END RSA PRIVATE KEY-----", "client_email": "example-project@appspot.gserviceaccount.com", "client_id": example-client", "auth_uri": "https://accounts.google.com/o/oauth2/auth", "token_uri": "https://oauth2.googleapis.com/token", "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs", "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/example-project%%40appspot.gserviceaccount.com", "universe_domain": "googleapis.com" } EOT ) }'

resource:
  aws_glue_connection:
    example:
      name: example
      connection_type: BIGQUERY
      connection_properties:
        SparkProperties: example-json-policy
```

## OpenSearch Service Connection

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: '{ "opensearch.net.http.auth.user" = "exampleusername" "opensearch.net.http.auth.pass" = "examplepassword" }'

resource:
  aws_glue_connection:
    example:
      name: example
      connection_type: OPENSEARCH
      connection_properties:
        SparkProperties: '{ "secretId": aws_secretsmanager_secret.example.name "opensearch.nodes"             = "https://search-exampledomain-ixlmh4jieahrau3bfebcgp8cnm.us-east-1.es.amazonaws.com" "opensearch.port"              = "443" "opensearch.aws.sigv4.region"  = "us-east-1" "opensearch.nodes.wan.only"    = "true" "opensearch.aws.sigv4.enabled" = "true" }'
```

## Snowflake Connection

```yaml
resource:
  aws_secretsmanager_secret:
    example:
      name: example-secret

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: '{ "sfUser": "exampleusername" "sfPassword": "examplepassword" }'

resource:
  aws_glue_connection:
    example:
      name: example
      connection_type: SNOWFLAKE
      connection_properties:
        SparkProperties: '{ "secretId": aws_secretsmanager_secret.example.name "sfRole": "EXAMPLEETLROLE" "sfUrl": "exampleorg-exampleconnection.snowflakecomputing.com" }'
```

## DynamoDB Connection

```yaml
resource:
  aws_glue_connection:
    test:
      name: example
      connection_type: DYNAMODB
      athena_properties:
        lambda_function_arn: "arn:aws:lambda:us-east-1:123456789012:function:athenafederatedcatalog_athena_abcdefgh"
        disable_spill_encryption: false
        spill_bucket: example-bucket
```
