# Use the kube-prometheus-stack to create an ingress

## Install the helm chart

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

## Show values and copy to a new file

`helm show values prometheus-community/kube-prometheus-stack` show all the default values of the kube-prometheus-stack

We can can pipe those values in a values.yaml file with the following command:

```bash
helm show values prometheus-community/kube-prometheus-stack > values.yaml
```
We will then use the values.yaml file to locate the grafana object and check the various keys and default values.

We can also generate an ingress with the following command:

```bash
kubectl create ingress NAME --rule=host/path=service:port[,tls[=secret]]  [options]
```

As example, I can generate the content of an ingress named `simple` with `grafana.dembasiby.tech` as host path and output it in to yaml with the following command:

```bash
kubectl create ingress simple --rule=grafana.dembasiby.tech/=svc1:8080,tls=my-cert --dry-run=client -o yaml
```

After adding the content of the ingress object, it's important to reconcile, ideally with source, using `flux`:

```bash
flux reconcile kustomization --with-source [kustomization name]
```


## Generate the Private Key and Certificate

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout ./tls.key \
  -out ./tls.crt \
  -subj "/C=SN/ST=Dakar/L=Dakar/O=Homelab Corps/OU=Department of Monitoring/CN=grafana.dembasiby.tech" \
  -addext "subjectAltName=DNS:grafana.dembasiby.tech"
```

## Create the secret

```bash
kubectl create secret tls grafana-tls-secret \
  --cert=~/tls.crt \
  --key=~/tls.key \
  --namespace=monitoring \
  --dry-run=client \
  -o yaml > monitoring/configs/staging/grafana-tls-secret.yaml
```

## Encrypt the data field with SOPS

We may first generate an age.agekey file that includes a public and private keys with the following command:

```bash 
age-keygen -o age.agekey
cat age.agekey # to view the content
```

```bash
export AGE_PUBLIC=[pubic key]

sops --age=$AGE_PUBLIC \
--encrypt --encrypted-regex '^(data|stringData)$' --in-place grafana-tls-secret.yaml

```
