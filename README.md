# helm-istio-service-mesh

## Installation steps

[1] Install the Istio base chart which contains cluster-wide resources used by the Istio control plane

```bash
helm upgrade -i istio-base charts/base -n istio-system
```
