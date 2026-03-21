# Amplify App

Manage Amplify App resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      repository: "https://github.com/example/app"
      build_spec: |
        version: 0.1
        frontend:
        phases:
        preBuild:
        commands:
        - yarn install
        build:
        commands:
        - yarn run build
        artifacts:
        baseDirectory: build
        files:
        - '**/*'
        cache:
        paths:
        - node_modules/**/*
      custom_rule:
        source: "/<*>"
        status: 404
        target: /index.html
      environment_variables:
        ENV: test
```

## Repository with Tokens

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      repository: "https://github.com/example/app"
      access_token: ...
```

## Auto Branch Creation

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      enable_auto_branch_creation: true
      auto_branch_creation_patterns:
        - "*"
        - "*/**"
      auto_branch_creation_config:
        enable_auto_build: true
```

## Basic Authorization

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      enable_basic_auth: true
      basic_auth_credentials: base64-encoded-content
```

## Rewrites and Redirects

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      custom_rule:
        source: "/api/<*>"
        status: 200
        target: "https://api.example.com/api/<*>"
      custom_rule:
        source: </^[^.]+$|\\.(?!(css|gif|ico|jpg|js|png|txt|svg|woff|ttf|map|json)$)([^.]+$)/>
        status: 200
        target: /index.html
```

## Custom Image

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      environment_variables: 
```

## Custom Headers

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      custom_headers: |
        customHeaders:
        - pattern: '**'
        headers:
        - key: 'Strict-Transport-Security'
        value: 'max-age=31536000; includeSubDomains'
        - key: 'X-Frame-Options'
        value: 'SAMEORIGIN'
        - key: 'X-XSS-Protection'
        value: '1; mode=block'
        - key: 'X-Content-Type-Options'
        value: 'nosniff'
        - key: 'Content-Security-Policy'
        value: "default-src 'self'"
```

## Job Config

```yaml
resource:
  aws_amplify_app:
    example:
      name: example
      job_config:
        build_compute_type: STANDARD_8GB
```
