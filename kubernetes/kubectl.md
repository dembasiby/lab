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
### Pod Creation or Update
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

### Adding A Specific Namespace
When we create a new pod, it is created in the default namespace. But we can specify a namespace with either `--namespace` or `-n` flags.

```bash
kubectl run [name] --image=[image] --namespace=[namespace]
```

We may want sometimes to change the default namespace. In this case, we can run the following command

```bash
kubectl config set-context --current --namespace=[namespace]
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

### Deployment Creation
We can also define new deployment definition in yaml.

```bash
kubectl create deployment [name] --image=[image] --replicas=[#replicas] --dry-run=client -o yaml > filename.yaml
```

Example

```bash
kubectl create deployment test --image=httpd --replicas=3 --dry-run=client -o yaml > test.yaml
```

This creates a new deployment `test` with 3 replicas with the following content.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  replicas: 3
  selector:
    matchLabels:
      app: test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test
    spec:
      containers:
      - image: httpd
        name: httpd
        resources: {}
status: {}
```


Once the deployment created, in the case of `Mealie`, we can access the app on our local network using port Forwarding.

```bash
kubectl port-forward pods/[pod] [port_number]
```


## List pods with ips, nods, etc. 

```bash
kubectl get pods -o wide
```

## Execute commands inside a pod 
```bash
kubectl exec -it [pod name] -- /bin/bash
```

A very interesting command is the `watch` command. The `man` page defines it as command that execute periodically, showing output on screen. Combined with `kubectl`, we can watch the execution of deployment, particularly with updates. 

```bash
watch -n 1 "kubectl get pods"
```

The above command will call the command in parenthesis every 1 second until we kill the process. Using it while introducing changes in a deployment file and reapplying it shows how `kubernetes` handle continuous deployment in real time. 

## Services
Get Services
```bash
kubectl get service [-o wide]
```

Create a new service from a deployment

```bash
kubectl expose deployment [deployment] --port=[port]
```
