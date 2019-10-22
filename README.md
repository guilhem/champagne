# Champagne 🍾

![logo](logo_small.png)

Kubernetes End-to-End testing

## Goal

Before going into production, you may want to validate all your deployment (services, pods, ingress…)

## Features

Detect errors for:

- pod
  - imagePullError
  - too long pending
  - restarting too quickly
- Connectivity
  - Services
  - Ingresses

## Getting started

Follow these instructions to get _champagne_ up and running.

### Prerequisites

- a Kubernetes cluster
- _kubeconfig_ configured

### Example

```
$ champagne test
```

## Configuration

### Services

By default, _champagne_ do a basic TCP check on service exposed port.

### Ingress

By default, _champagne_ check HTTP code return by exposed Ingresses

You can customized it with annotations:

```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    champagne.barpilot.io/error-codes: "5xx,404"
    champagne.barpilot.io/timeout: 100s
spec:
  rules:
  - http:
      paths:
      - path: /testpath
        backend:
          serviceName: test
          servicePort: 80
```
