# Helm

The package manager for Kubernetes

## Create a helm chart

`helm create [chart name]`

## Install a chart
Install a chart from a template

`helm install [release-name] [chart folder] [set options with the --set flag]`

## Upgrade a chart

We can upgrade a chart with `helm upgrade [chart] [repo]`. 

Example:

`helm upgrade wordpress-release bitnami/worpress`



