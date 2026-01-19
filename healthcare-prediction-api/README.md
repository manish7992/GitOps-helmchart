# Healthcare Prediction API Helm Chart

This Helm chart deploys the Healthcare Prediction API, a FastAPI-based service with monitoring and security features.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- LoadBalancer service support (for external access)

## Installing the Chart

To install the chart with the release name `my-healthcare-api`:

```bash
helm install my-healthcare-api ./healthcare-prediction-api
```

## Configuration

The following table lists the configurable parameters:

### Global Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `3` |
| `image.repository` | Image repository | `healthcare-prediction-api` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `Always` |

### Service Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `service.type` | Kubernetes service type | `LoadBalancer` |
| `service.port` | Service port | `80` |
| `service.targetPort` | Container target port | `8000` |

### Ingress Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `ingress.enabled` | Enable ingress controller resource | `true` |
| `ingress.className` | Ingress class name | `alb` |
| `ingress.hosts[0].host` | Default host for the ingress | `api.healthcare.example.com` |

## Examples

### Installing with custom values

```bash
helm install my-healthcare-api ./healthcare-prediction-api -f values-prod.yaml
```

### Upgrading the deployment

```bash
helm upgrade my-healthcare-api ./healthcare-prediction-api --set image.tag=v1.3.0
```

## Testing

Test the chart template rendering:

```bash
helm template my-healthcare-api ./healthcare-prediction-api
```

## Monitoring

The chart includes:
- ServiceMonitor for Prometheus
- Metrics endpoint at `/metrics`
- Health check endpoint at `/health`

## Security Features

- Network policies for traffic control
- RBAC with minimal permissions
- Pod security contexts
- Read-only root filesystem
- Non-root user execution