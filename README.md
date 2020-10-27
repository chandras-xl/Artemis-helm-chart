# Artemis-helm-chart
Artemis helm chart to deploy messaging cluster on k8s's

The helm chart is a fork of below repository with few modification in the below files.<br>
`master-configmap.yaml`<br>
`master-statefulset.yaml`<br>
`slave-statefulset.yaml`<br>

https://github.com/vromero/activemq-artemis-helm

# Configuration
To see the lists of configurable parameters of this chart and their default values please refer to above repo link.

# Installing the Chart
```bash
git clone https://github.com/chandras-xl/Artemis-helm-chart.git
```
```bash
helm install activemq-artemis Artemis-helm-chart/
```
# Uninstalling the Chart
```bash
helm uninstall activemq-artemis
```
# Limitations of the chart
1. ScaleOut of pods doesn't work as the Artemis cluster is created using static connectors. If we try to scale out the pod it will be scalled but it won't be a part of the cluster (The fact that static connectors used is to avoid the multicasting issues on the cloud platforms.)
2. In order for failover and failback to work we need to use persistent storage in our k8s cluster. so If you don’t have any kind of persistent storage inside your k8s cluster, then the alternative is to move your cluster formation of Aretmis to virtual machine I.e as docker image (docker-compose) or run as a daemon.
