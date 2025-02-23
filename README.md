# eks-app-helm-chart: Deploying Applications on Amazon EKS with Helm

This document provides the configuration details for the `eks-app-helm-chart`.
The chart creates a deployment, a service, a pod disruption budget, an ingress resource, and HPA.

## Amazon EKS Auto Mode

If you are using EKS Auto Mode this chart is application ready. You can deploy the chart as is, and it will create the necessary resources for you.

- IngressClass Controller: `eks.amazonaws.com/alb` by default, if you are using a different ingress controller, you can change the `ingressClass.controller` value.
- Ingress Annotations: since the default IngressClass Controller is `eks.amazonaws.com/alb`, the default annotations are set to `alb.ingress.kubernetes.io/target-type: ip` and `alb.ingress.kubernetes.io/scheme: internet-facing`. If you are using a different ingress controller, you can change the `ingress.annotations` value. 
  - More information on the annotations can be found [here](https://docs.aws.amazon.com/eks/latest/userguide/auto-elb-example.html).
- Learn more about EKS Auto Mode [here](https://blog.awsfanboy.com/lets-explore-amazon-eks-auto-mode).
- EKS Auto Mode official documentation can be found [here](https://docs.aws.amazon.com/eks/latest/userguide/eks-auto-mode.html).

## Prerequisites

- Kubernetes 1.29+
- Helm 3.0+
- ingressCalass is a cluster-scoped resource. Since this chart creates an ingressClass resource, and you need to have the necessary permissions to create it.

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter                         | Description                                | Default                 |
|-----------------------------------|--------------------------------------------|-------------------------|
| `namePrefix`                      | Prefix for resource names                  | `devopswithzack`        |
| `namespace`                       | Namespace                                  | `default`               |
| `image.repository`                | Image repository                           | `awsfanboy/doggo-app`   |
| `image.tag`                       | Image tag                                  | `latest`                |
| `image.pullPolicy`                | Image pull policy                          | `IfNotPresent`          |
| `resources.requests.cpu`          | CPU resource requests                      | `100m`                  |
| `resources.requests.memory`       | Memory resource requests                   | `128Mi`                 |
| `resources.limits.cpu`            | CPU resource limits                        | `200m`                  |
| `resources.limits.memory`         | Memory resource limits                     | `256Mi`                 |
| `replicaCount`                    | Number of replicas                         | `6`                     |
| `service.name`                    | Service name                               | `zack-service`          |
| `service.type`                    | Service type                               | `NodePort`              |
| `service.port`                    | Service port                               | `80`                    |
| `service.targetPort`              | Target port                                | `80`                    |
| `podDisruptionBudget.minAvailable`| Minimum available pods                     | `80%`                   |
| `ingress.name`                    | Ingress name                               | `zack-ingress`          |
| `ingress.className`               | Ingress class name                         | `eks-auto-alb`          |
| `ingress.annotations`             | Ingress annotations                        | `{}`                    |
| `ingress.path`                    | Ingress path                               | `/`                     |
| `ingress.pathType`                | Ingress path type                          | `Prefix`                |
| `ingressClass.name`               | Ingress class name                         | `eks-auto-alb`          |
| `ingressClass.controller`         | Ingress class controller                   | `eks.amazonaws.com/alb` |
| `hpa.enabled`                     | Enable HPA                                 | `true`                  |
| `hpa.minReplicas`                 | Minimum replicas                           | `3`                     |
| `hpa.maxReplicas`                 | Maximum replicas                           | `12`                    |
| `hpa.targetCPUUtilizationPercentage`| Target CPU utilization percentage         | `50`                    |

### Deploying the Application

To deploy the application, use the following command:

```sh
helm install my-release ./eks-app-helm-chart
```

### Contrubution Guidelines
- This is for the community, by the community. Please contribute by raising issues, pull requests, and sharing your feedback.

### DevOps with Zack

<a href="https://awsfanboy.com/">
  <img src="https://awsfanboy.com/assets/devops_with_zack.jpg" alt="DevOps with Zack" width="300"/>
</a>
