# OpenTelemetry Tracing

ytofu supports OpenTelemetry for distributed tracing, enabling observability of infrastructure operations across your deployment pipeline.

## Overview

OpenTelemetry tracing provides:
- Visibility into operation timing
- Debugging of slow or failing operations
- Integration with observability platforms
- Performance analysis of infrastructure changes

## Enabling Tracing

Configure tracing via environment variables:

```bash
# Enable OTLP exporter
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"

# Set service name
export OTEL_SERVICE_NAME="ytofu"

# Run ytofu with tracing
ytofu apply
```

## Configuration Options

### OTLP Endpoint

Set the OpenTelemetry collector endpoint:

```bash
# gRPC endpoint (default)
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"

# HTTP endpoint
export OTEL_EXPORTER_OTLP_PROTOCOL="http/protobuf"
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4318"
```

### Service Identity

Configure how ytofu identifies itself:

```bash
export OTEL_SERVICE_NAME="ytofu"
export OTEL_SERVICE_VERSION="1.11.0"
```

### Resource Attributes

Add custom attributes to all spans:

```bash
export OTEL_RESOURCE_ATTRIBUTES="environment=production,team=platform"
```

### Sampling

Control trace sampling rate:

```bash
# Sample all traces (default)
export OTEL_TRACES_SAMPLER="always_on"

# Sample 10% of traces
export OTEL_TRACES_SAMPLER="traceidratio"
export OTEL_TRACES_SAMPLER_ARG="0.1"

# Never sample (disable tracing)
export OTEL_TRACES_SAMPLER="always_off"
```

## Trace Structure

ytofu creates spans for major operations:

```
ytofu.apply
├── ytofu.init
│   ├── provider.download
│   └── provider.initialize
├── ytofu.refresh
│   └── provider.read_resource (per resource)
├── ytofu.plan
│   ├── config.load
│   ├── graph.build
│   └── graph.walk
└── ytofu.apply
    ├── resource.create (per resource)
    ├── resource.update (per resource)
    └── resource.delete (per resource)
```

## Integration Examples

### Jaeger

Send traces to Jaeger:

```bash
# Start Jaeger
docker run -d --name jaeger \
  -p 16686:16686 \
  -p 4317:4317 \
  jaegertracing/all-in-one:latest

# Configure ytofu
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
export OTEL_SERVICE_NAME="ytofu"

# Run ytofu
ytofu apply

# View traces at http://localhost:16686
```

### Grafana Tempo

Send traces to Grafana Tempo:

```bash
export OTEL_EXPORTER_OTLP_ENDPOINT="http://tempo.monitoring:4317"
export OTEL_SERVICE_NAME="ytofu"
```

### Datadog

Send traces to Datadog:

```bash
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
export OTEL_SERVICE_NAME="ytofu"
export DD_OTLP_CONFIG_RECEIVER_PROTOCOLS_GRPC_ENDPOINT="0.0.0.0:4317"
```

### AWS X-Ray

Send traces to AWS X-Ray via the ADOT collector:

```bash
export OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317"
export OTEL_SERVICE_NAME="ytofu"
export OTEL_PROPAGATORS="xray"
```

### Honeycomb

Send traces to Honeycomb:

```bash
export OTEL_EXPORTER_OTLP_ENDPOINT="https://api.honeycomb.io"
export OTEL_EXPORTER_OTLP_HEADERS="x-honeycomb-team=YOUR_API_KEY"
export OTEL_SERVICE_NAME="ytofu"
```

## CI/CD Integration

### GitHub Actions

```yaml
name: Deploy Infrastructure
on: push

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Start OTEL Collector
        run: |
          docker run -d --name otel-collector \
            -p 4317:4317 \
            otel/opentelemetry-collector:latest

      - name: Deploy with Tracing
        env:
          OTEL_EXPORTER_OTLP_ENDPOINT: "http://localhost:4317"
          OTEL_SERVICE_NAME: "ytofu-ci"
          OTEL_RESOURCE_ATTRIBUTES: "ci.pipeline=${{ github.run_id }}"
        run: |
          ytofu init
          ytofu apply -auto-approve
```

### GitLab CI

```yaml
deploy:
  stage: deploy
  variables:
    OTEL_EXPORTER_OTLP_ENDPOINT: "http://otel-collector:4317"
    OTEL_SERVICE_NAME: "ytofu-gitlab"
    OTEL_RESOURCE_ATTRIBUTES: "ci.pipeline=$CI_PIPELINE_ID"
  script:
    - ytofu init
    - ytofu apply -auto-approve
```

## Analyzing Traces

### Identifying Slow Operations

Look for spans with long durations:
- Provider initialization
- API calls to cloud providers
- Resource creation/updates

### Finding Failures

Failed operations include error attributes:
- `error=true`
- `error.message`
- `error.type`

### Correlating with Logs

Use trace IDs to correlate with log entries:

```bash
export OTEL_LOG_LEVEL="debug"
export TF_LOG="DEBUG"
```

## Custom Span Attributes

ytofu adds relevant attributes to spans:

| Attribute | Description |
|-----------|-------------|
| `resource.type` | Resource type (e.g., `aws_instance`) |
| `resource.name` | Resource name |
| `provider.name` | Provider name |
| `operation` | Operation type (create, read, update, delete) |

## Performance Overhead

Tracing adds minimal overhead:
- Span creation: ~1-5 microseconds per span
- Export: Batched asynchronously
- Memory: Small buffer for pending spans

For production use, consider sampling to reduce volume.

## Disabling Tracing

To completely disable tracing:

```bash
export OTEL_SDK_DISABLED="true"
```

Or use the always-off sampler:

```bash
export OTEL_TRACES_SAMPLER="always_off"
```

## Related

- [Resource Lifecycle](resource-lifecycle.md)
- [Testing](testing.md)
