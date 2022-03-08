# prometheus-setup

% helm dependency update ./prometheus

% helm install test --dry-run --debug ./prometheus

% helm dependency update ./prometheus-adapter

% helm install test --dry-run --debug ./prometheus-adapter

% helm install promotheus-8mar ./prometheus

% helm install promotheus-adapter-8mar ./prometheus-adapter

Promotheus:

% export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")

% kubectl --namespace default port-forward $POD_NAME 9091

Metrics:

% kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1
