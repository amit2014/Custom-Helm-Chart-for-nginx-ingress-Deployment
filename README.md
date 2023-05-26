# Custom Helm Chart for nginx-ingress Deployment

This repository contains a custom Helm chart for deploying nginx-ingress with custom variables. The chart is named `infra-nginx-ingress-trial` and allows you to expose specific ingresses based on the `nginx-trial` annotation.

## Prerequisites

To use this Helm chart, ensure you have the following prerequisites installed:

- Kubernetes cluster (e.g., Docker Desktop with Kubernetes enabled)
- Helm (version 3 or later)

## Installation

1. Clone this repository to your local machine:

```bash
git clone https://github.com/your-username/infra-nginx-ingress-trial
cd infra-nginx-ingress-trial
```
2. Update the chart values in `values.yaml` according to your requirements. You can modify variables such as `replicaCount`, `service.type`, `ingress.annotations`, and more.

3. Deploy the nginx-ingress chart using Helm:
```bash
helm install infra-nginx-ingress-trial ./infra-nginx-ingress-trial
```
4. Verify that the nginx-ingress controller is running:
```bash
kubectl get pods -l app.kubernetes.io/name=infra-nginx-ingress-trial
```
## Configuration

The following table lists the configurable parameters and their default values in the `values.yaml` file:

| Parameter  | Description  | Default |
| --------- | --------- | --------- |
| replicaCount | Number of nginx-ingress replicas to deploy | 1 |
| image.repository | nginx-ingress image repository | nginx/nginx-ingress  |
| image.tag | nginx-ingress image tag | 1.0.0  |
| service.type | Kubernetes service type for the nginx-ingress | LoadBalancer  |
| ingress.annotations |	Annotations to filter specific ingresses |  nginx-trial  |

Feel free to modify the values according to your specific deployment requirements.

## Exposing Ingresses
To expose ingresses using the nginx-ingress controller, follow these steps:

1. Annotate your ingresses with `nginx-trial` to indicate that they should be handled by this nginx-ingress controller. For example:
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx-trial: "true"
...
```
2. Apply the annotated ingress manifest to your Kubernetes cluster:
```bash
kubectl apply -f my-ingress.yaml
```
The nginx-ingress controller deployed using this custom chart will only search for ingresses with the `nginx-trial` annotation and expose them accordingly.

## Cleanup
To remove the nginx-ingress deployment and associated resources, run the following Helm command:
```bash
helm uninstall infra-nginx-ingress-trial
```
This will remove the nginx-ingress deployment from your Kubernetes cluster.

## Conclusion
This custom Helm chart provides an easy and configurable way to deploy the nginx-ingress controller with support for exposing specific ingresses based on annotations. Feel free to explore the chart and adjust the values to suit your deployment needs.

If you have any questions or encounter any issues, please feel free to open an issue in this repository.
