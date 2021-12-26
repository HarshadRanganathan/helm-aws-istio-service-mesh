# helm-aws-istio-service-mesh

Heml chart for installing Istio service mesh in the kubernetes cluster

## Dependencies

[1] https://github.com/HarshadRanganathan/helm-aws-load-balancer-controller

### Config Updates

In `shared-values.yaml` file available inside `charts/istiod/stages` folder, add values for below settings:

|||
|--|--|
|tracer.zipkin.address |Update the tracer address e.g. jaegar |

## Installation steps

[1] Install the Istio base chart which contains cluster-wide resources used by the Istio control plane

```bash
helm upgrade -i istio-base charts/base -n istio-system
```

[2] Install the Istio discovery chart which deploys the istiod service

```
helm upgrade -i istiod charts/istiod -n istio-system --values=charts/istiod/stages/shared-values.yaml
```

[3] Install the Istio gateway chart which deploys the gateway service

```
helm upgrade -i istio-gateway charts/gateways/istio-ingress -n istio-system --values=charts/gateways/istio-ingress/stages/shared-values.yaml --values=charts/gateways/istio-ingress/stages/prod/prod-values.yaml
```

## Automatic Sidecar Injection

To inject sidecar to any of the new pods that get created, set label `istio-injection=enabled` to the namespace.

```
kubectl label namespace <namespace> istio-injection=enabled --overwrite
```
