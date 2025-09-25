# Helm

The package manager for Kubernetes


## Install Homarr
`Homarr` is a modern dashboard for managing your apps and services in one place.

```bash
helm repo add homarr-labs https://homarr-labs.github.io/charts/
helm repo update
helm install homarr homarr-labs/homarr --namespace homarr --create-namespace
```

## Homarr After-Installation Steps

```bash

kubectl create secret generic db-secret --from-literal=db-encryption-key=$(openssl rand -hex 32) --namespace homarr

export POD_NAME=$(kubectl get pods --namespace homarr -l "app.kubernetes.io/name=homarr,app.kubernetes.io/instance=homarr" -o jsonpath="{.items[0].metadata.name}")

export CONTAINER_PORT=$(kubectl get pod --namespace homarr $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")

echo "Visit http://127.0.0.1:8080 to use your application"

kubectl --namespace homarr port-forward $POD_NAME 8080:$CONTAINER_PORT
```

