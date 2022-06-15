-  #### Install loki-stack grafana
```
helm show values grafana/loki-stack > loki-stack.yaml
helm install loki-stack grafana/loki-stack --values loki-stack.yaml -n loki --create-namespace
