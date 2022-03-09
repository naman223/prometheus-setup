# prometheus-setup

**Steps to execute:**

1. helm dependency update ./prometheus
2. helm install test --dry-run --debug ./prometheus
3. helm dependency update ./prometheus-adapter
4. helm install test --dry-run --debug ./prometheus-adapter
5. helm install <release_name_server> ./prometheus
6. helm install <release_name_adapter> ./prometheus-adapter

**Prometheus Port forward to see Metrics**:
```bash
export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")

kubectl --namespace default port-forward $POD_NAME 9090 &
```

**Metrics**:
```bash
kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1

curl http://localhost:9090/metrics/
```

**Add below annotations to the pod which needs to push metrics:**
```bash
annotations:
  prometheus.io/path: /api/metrics
  prometheus.io/port: "8080"
  prometheus.io/scrape: "true"
```

**Custom metrics:**
```bash
curl http://localhost:9090/api/v1/query?query=string_latency_seconds_sum
```

**System metrics:**
```bash
curl http://localhost:9090/api/v1/query?query=requests_in_progress_total
```

**Note:**

Check the alertmanager log in default namespace. If it's failing then edit alertmanager deployment and update endpoint for prometheus server with IP address of prometheus server service as below
```bash
url: http://prometheus.default.svc:80
```
should be 
```bash
url: http://ip_address_of_prometheus_server_service:80
```