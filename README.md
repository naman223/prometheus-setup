# prometheus-setup

% helm dependency update ./prometheus

% helm install test --dry-run --debug ./prometheus

% helm dependency update ./prometheus-adapter

% helm install test --dry-run --debug ./prometheus-adapter

% helm install promotheus-8mar ./prometheus

% helm install promotheus-adapter-8mar ./prometheus-adapter

Promotheus:

% export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")

% kubectl --namespace default port-forward $POD_NAME 9090 &

Metrics:

% kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1

% curl http://localhost:9090/metrics/

Add annotations to the pod for pushing image:
annotations:
  prometheus.io/path: /api/metrics
  prometheus.io/port: "8080"
  prometheus.io/scrape: "true"

Custom metrics:
% curl http://localhost:9090/api/v1/query?query=string_latency_seconds_sum

System metrics:
% curl http://localhost:9090/api/v1/query?query=requests_in_progress_total

Check the alertmanager log and if it's failing then edit alertmanager deployment and update endpoint for prometheus server with IP address of prometheus server.
url: http://prometheus.default.svc:80 - shoud be http://<ip address>:80>
