# helm-istio-service-mesh

## Installation steps

[1] Install the Istio base chart which contains cluster-wide resources used by the Istio control plane

```bash
helm upgrade -i istio-base charts/base -n istio-system
```

[3] Install the Istio gateway chart which deploys the gateway service

```
helm upgrade -i istio-gateway charts/gateways/istio-ingress -n istio-system --values=charts/gateways/istio-ingress/stages/shared-values.yaml
```
