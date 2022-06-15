#### Install loki-stack grafana
```
helm show values grafana/loki-stack > loki-stack.yaml
helm install loki-stack grafana/loki-stack --values loki-stack.yaml -n loki --create-namespace
```

```
kubectl get sc
NAME                 PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
standard (default)   rancher.io/local-path   Delete          WaitForFirstConsumer   false                  85m
kubectl get pvc -n loki
NAME                   STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
storage-loki-stack-0   Bound    pvc-1a84b2b5-be5b-4d90-918b-143bca0185fb   1Gi        RWO            standard       71m
kubectl get all -n loki
NAME                                      READY   STATUS    RESTARTS   AGE
pod/loki-stack-0                          1/1     Running   0          71m
pod/loki-stack-grafana-54db74bd4f-x4c9n   2/2     Running   0          58m
pod/loki-stack-promtail-hqxvw             1/1     Running   0          71m

NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/loki-stack            ClusterIP   10.96.190.168   <none>        3100/TCP   71m
service/loki-stack-grafana    ClusterIP   10.96.189.147   <none>        80/TCP     70m
service/loki-stack-headless   ClusterIP   None            <none>        3100/TCP   71m

NAME                                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/loki-stack-promtail   1         1         1       1            1           <none>          71m

NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/loki-stack-grafana   1/1     1            1           70m

NAME                                            DESIRED   CURRENT   READY   AGE
replicaset.apps/loki-stack-grafana-54db74bd4f   1         1         1       58m
replicaset.apps/loki-stack-grafana-856bc6bf5c   0         0         0       70m

NAME                          READY   AGE
statefulset.apps/loki-stack   1/1     71m
