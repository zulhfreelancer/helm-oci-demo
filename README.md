## About

To learn how to deploy a Helm chart to OCI registries (Docker Hub in this case).

## Publish Commands

```sh
cd /path/to/this/repo

helm package .

export DOCKER_USERNAME="something"

helm registry login registry-1.docker.io -u $DOCKER_USERNAME

helm push helm-oci-demo-0.0.0.tgz oci://registry-1.docker.io/$DOCKER_USERNAME
```

> For the registry password, an [access token](https://app.docker.com/settings/personal-access-tokens) with "Read & Write" permission is required.

## Usage Commands

```sh
kind create cluster --name helm-oci-demo

export DOCKER_USERNAME="something"

helm install helm-oci-demo oci://registry-1.docker.io/$DOCKER_USERNAME/helm-oci-demo --version 0.0.0

# should return "helm-oci-demo" release, with "deployed" status and the chart is "helm-oci-demo-0.0.0"
helm ls

# should return three "demo-*" pods
kubectl get pods

# should return "demo" service with type of LoadBalancer
kubectl get svc
```

## References

- https://cyclops-ui.com/blog/2024/01/29/OCI-based-registries/
