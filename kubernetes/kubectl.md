## Get the current context
```bash
# Get the current context (Minikube, Rancher Desktop, etc.)
kubectl config current-context
```

## Bash autocompletion
```bash
source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.
```

## Generate yaml definition
```bash
kubectl run [name] --image=[image] --dry-run=client -o yaml
```

Example:
```bash
kubectl run nginx-yaml --image=nginx --dry-run=client -o yaml
```

The command will generate the following content. We can just follow with `>>` and the name of our file or create a new file.

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-yaml
  name: nginx-yaml
spec:
  containers:
  - image: nginx
    name: nginx-yaml
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Create/update a pod from a yaml file
Once the file create or updated, we can use the `create` commands:

```bash
kubectl create -f [filename]
```

We can also use `apply` which either create a new pod if it doesn't exist or update it if it does.

```bash
kubectl apply -f [filename]
```

## List pods with ips, nods, etc. 

```bash
kubectl get pods -o wide
```

## Execute commands inside a pod 
```bash
kubectl exec -it [pod name] -- /bin/bash
```
```
```


