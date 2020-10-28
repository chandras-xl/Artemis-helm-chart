# Artemis-helm-chart
Artemis helm chart to deploy messaging cluster on k8s's

The helm chart is a fork of below repository with few modification in the below files to fix the failover and failback issue.<br>
`master-configmap.yaml`<br>
`master-statefulset.yaml`<br>
`slave-statefulset.yaml`<br>

https://github.com/vromero/activemq-artemis-helm

# Configuration
The following tables lists the configurable parameters for the chart and their default values.

| Parameter                            | Description                           | Default                                                    |
| ------------------------------------ | ------------------------------------- | ---------------------------------------------------------- |
| `imageTag`                           | `xl-docker.xebialabs.com/artemis-docker-image` image tag. | 2.15.0                                        |
| `imagePullPolicy`                    | Image pull policy                     | `IfNotPresent`                                             |
| `artemisUser`                        | Username of new user to create.       | `artemis`                                                  |
| `artemisPassword`                    | Password for the new user.            | `artemis`                                            |
| `replicas`                           | Number of nodes in the cluster.       | 2                                                          |
| `persistence.enabled`                | Create a volume to store data         | true                                                       |
| `persistence.size`                   | Size of persistent volume claim       | 8Gi RW                                                     |
| `persistence.storageClass`           | Type of persistent volume claim       | nil  (uses alpha storage class annotation)                 |
| `persistence.accessMode`             | ReadWriteOnce or ReadOnly             | ReadWriteOnce                                              |
| `persistence.testJournalPerformance` | See docker image docs                 | `AUTO`                                                     |
| `resources.request.memory`           | Memory resource requests/limits       | `256Mi`                                                    |
| `resources.request.cpu`              | CPU/Memory resource requests/limits   | `100m`                                                     |

For more details please visit below repo link.<br>
https://github.com/vromero/activemq-artemis-helm

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
