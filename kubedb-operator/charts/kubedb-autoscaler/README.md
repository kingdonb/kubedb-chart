# KubeDB Autoscaler

[KubeDB Autoscaler by AppsCode](https://github.com/kubedb) - Autoscale KubeDB operated Databases

## TL;DR;

```console
$ helm repo add appscode https://charts.appscode.com/stable/
$ helm repo update
$ helm install kubedb-autoscaler appscode/kubedb-autoscaler -n kube-system
```

## Introduction

This chart deploys a KubeDB Autoscaler operator on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.12+

## Installing the Chart

To install the chart with the release name `kubedb-autoscaler`:

```console
$ helm install kubedb-autoscaler appscode/kubedb-autoscaler -n kube-system
```

The command deploys a KubeDB Autoscaler operator on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `kubedb-autoscaler`:

```console
$ helm delete kubedb-autoscaler -n kube-system
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the `kubedb-autoscaler` chart and their default values.

|                Parameter                 |                                                                                                                                                                                 Description                                                                                                                                                                                  |                                Default                                |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| nameOverride                             | Overrides name template                                                                                                                                                                                                                                                                                                                                                      | `""`                                                                  |
| fullnameOverride                         | Overrides fullname template                                                                                                                                                                                                                                                                                                                                                  | `""`                                                                  |
| replicaCount                             | Number of KubeDB operator replicas to create (only 1 is supported)                                                                                                                                                                                                                                                                                                           | `1`                                                                   |
| license                                  | License for the product. Get a license by following the steps from [here](https://stash.run/docs/latest/setup/install/enterprise#get-a-trial-license). <br> Example: <br> `helm install appscode/kubedb-autoscaler \` <br> `--set-file license=/path/to/license/file` <br> `or` <br> `helm install appscode/kubedb-autoscaler \` <br> `--set license=<license file content>` | `""`                                                                  |
| updateInterval                           | Interval between each autoscaler loop                                                                                                                                                                                                                                                                                                                                        | `1m`                                                                  |
| registryFQDN                             | Docker registry fqdn used to pull KubeDB related images. Set this to use docker registry hosted at ${registryFQDN}/${registry}/${image}                                                                                                                                                                                                                                      | `""`                                                                  |
| operator.registry                        | Docker registry used to pull KubeDB enterprise operator image                                                                                                                                                                                                                                                                                                                | `kubedb`                                                              |
| operator.repository                      | KubeDB enterprise operator container image                                                                                                                                                                                                                                                                                                                                   | `kubedb-autoscaler`                                                   |
| operator.tag                             | KubeDB enterprise operator container image tag                                                                                                                                                                                                                                                                                                                               | `v0.6.0`                                                              |
| operator.resources                       | Compute Resources required by the enterprise operator container                                                                                                                                                                                                                                                                                                              | `{}`                                                                  |
| operator.securityContext                 | requests: cpu: 100m memory: 128Mi Security options the enterprise operator container should run with                                                                                                                                                                                                                                                                         | `{}`                                                                  |
| cleaner.registry                         | Docker registry used to pull Webhook cleaner image                                                                                                                                                                                                                                                                                                                           | `appscode`                                                            |
| cleaner.repository                       | Webhook cleaner container image                                                                                                                                                                                                                                                                                                                                              | `kubectl`                                                             |
| cleaner.tag                              | Webhook cleaner container image tag                                                                                                                                                                                                                                                                                                                                          | `v1.16`                                                               |
| cleaner.skip                             | Skip generating cleaner YAML                                                                                                                                                                                                                                                                                                                                                 | `false`                                                               |
| imagePullSecrets                         | Specify an array of imagePullSecrets. Secrets must be manually created in the namespace. <br> Example: <br> `helm template charts/kubedb-autoscaler \` <br> `--set imagePullSecrets[0].name=sec0 \` <br> `--set imagePullSecrets[1].name=sec1`                                                                                                                               | `[]`                                                                  |
| imagePullPolicy                          | Container image pull policy                                                                                                                                                                                                                                                                                                                                                  | `IfNotPresent`                                                        |
| criticalAddon                            | If true, installs KubeDB operator as critical addon                                                                                                                                                                                                                                                                                                                          | `false`                                                               |
| logLevel                                 | Log level for operator                                                                                                                                                                                                                                                                                                                                                       | `3`                                                                   |
| annotations                              | Annotations applied to operator deployment                                                                                                                                                                                                                                                                                                                                   | `{}`                                                                  |
| podAnnotations                           | Annotations passed to operator pod(s).                                                                                                                                                                                                                                                                                                                                       | `{}`                                                                  |
| nodeSelector                             | Node labels for pod assignment                                                                                                                                                                                                                                                                                                                                               | `{"beta.kubernetes.io/arch":"amd64","beta.kubernetes.io/os":"linux"}` |
| tolerations                              | Tolerations for pod assignment                                                                                                                                                                                                                                                                                                                                               | `[]`                                                                  |
| affinity                                 | Affinity rules for pod assignment                                                                                                                                                                                                                                                                                                                                            | `{}`                                                                  |
| podSecurityContext                       | Security options the operator pod should run with.                                                                                                                                                                                                                                                                                                                           | `{}`                                                                  |
| serviceAccount.create                    | Specifies whether a service account should be created                                                                                                                                                                                                                                                                                                                        | `true`                                                                |
| serviceAccount.annotations               | Annotations to add to the service account                                                                                                                                                                                                                                                                                                                                    | `{}`                                                                  |
| serviceAccount.name                      | The name of the service account to use. If not set and create is true, a name is generated using the fullname template                                                                                                                                                                                                                                                       | ``                                                                    |
| apiserver.groupPriorityMinimum           | The minimum priority the webhook api group should have at least. Please see https://github.com/kubernetes/kube-aggregator/blob/release-1.9/pkg/apis/apiregistration/v1beta1/types.go#L58-L64 for more information on proper values of this field.                                                                                                                            | `10000`                                                               |
| apiserver.versionPriority                | The ordering of the webhook api inside of the group. Please see https://github.com/kubernetes/kube-aggregator/blob/release-1.9/pkg/apis/apiregistration/v1beta1/types.go#L66-L70 for more information on proper values of this field                                                                                                                                         | `15`                                                                  |
| apiserver.enableMutatingWebhook          | If true, mutating webhook is configured for KubeDB CRDss                                                                                                                                                                                                                                                                                                                     | `true`                                                                |
| apiserver.enableValidatingWebhook        | If true, validating webhook is configured for KubeDB CRDss                                                                                                                                                                                                                                                                                                                   | `false`                                                               |
| apiserver.ca                             | CA certificate used by the Kubernetes api server. This field is automatically assigned by the operator.                                                                                                                                                                                                                                                                      | `not-ca-cert`                                                         |
| apiserver.bypassValidatingWebhookXray    | If true, bypasses checks that validating webhook is actually enabled in the Kubernetes cluster.                                                                                                                                                                                                                                                                              | `false`                                                               |
| apiserver.useKubeapiserverFqdnForAks     | If true, uses kube-apiserver FQDN for AKS cluster to workaround https://github.com/Azure/AKS/issues/522 (default true)                                                                                                                                                                                                                                                       | `true`                                                                |
| apiserver.healthcheck.enabled            | healthcheck configures the readiness and liveliness probes for the operator pod.                                                                                                                                                                                                                                                                                             | `false`                                                               |
| apiserver.port                           | Port used to expose the operator apiserver                                                                                                                                                                                                                                                                                                                                   | `8443`                                                                |
| apiserver.servingCerts.generate          | If true, generates on install/upgrade the certs that allow the kube-apiserver (and potentially ServiceMonitor) to authenticate operators pods. Otherwise specify certs in `apiserver.servingCerts.{caCrt, serverCrt, serverKey}`.                                                                                                                                            | `true`                                                                |
| apiserver.servingCerts.caCrt             | CA certficate used by serving certificate of webhook server.                                                                                                                                                                                                                                                                                                                 | `""`                                                                  |
| apiserver.servingCerts.serverCrt         | Serving certficate used by webhook server.                                                                                                                                                                                                                                                                                                                                   | `""`                                                                  |
| apiserver.servingCerts.serverKey         | Private key for the serving certificate used by webhook server.                                                                                                                                                                                                                                                                                                              | `""`                                                                  |
| enableAnalytics                          | If true, sends usage analytics                                                                                                                                                                                                                                                                                                                                               | `true`                                                                |
| monitoring.enabled                       | If true, enables monitoring KubeDB operator                                                                                                                                                                                                                                                                                                                                  | `false`                                                               |
| monitoring.agent                         | Name of monitoring agent ("prometheus.io" or "prometheus.io/operator" or "prometheus.io/builtin")                                                                                                                                                                                                                                                                            | `""`                                                                  |
| monitoring.serviceMonitor.labels         | Specify the labels for ServiceMonitor. Prometheus crd will select ServiceMonitor using these labels. Only usable when monitoring agent is `prometheus.io/operator`.                                                                                                                                                                                                          | `{}`                                                                  |
| additionalPodSecurityPolicies            | Additional psp names passed to operator <br> Example: <br> `helm template ./chart/kubedb-autoscaler \` <br> `--set additionalPodSecurityPolicies[0]=abc \` <br> `--set additionalPodSecurityPolicies[1]=xyz`                                                                                                                                                                 | `[]`                                                                  |
| storageAutoscaler.prometheus.address     | Prometheus address for storage metrics                                                                                                                                                                                                                                                                                                                                       | `http://prometheus-operated.monitoring.svc:9090`                      |
| storageAutoscaler.prometheus.bearerToken | Bearer token for prometheus server                                                                                                                                                                                                                                                                                                                                           | `""`                                                                  |
| storageAutoscaler.prometheus.caCert      | CA cert for prometheus server TLS connections                                                                                                                                                                                                                                                                                                                                | `""`                                                                  |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```console
$ helm install kubedb-autoscaler appscode/kubedb-autoscaler -n kube-system --set replicaCount=1
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while
installing the chart. For example:

```console
$ helm install kubedb-autoscaler appscode/kubedb-autoscaler -n kube-system --values values.yaml
```