# web-deployment-istio-ingress

This template generates Kubernetes manifests for a simple web deployment in an [Istio](https://istio.io/latest/docs/) enabled cluster using [Cookiecutter](https://cookiecutter.readthedocs.io/en/1.7.3/README.html).

By using this tool, you'll be prompted to enter values for your application, but can accept sensible default values.

For more control, you can create a [User Config](https://cookiecutter.readthedocs.io/en/1.7.3/advanced/user_config.html) file to pre-populate settings suitable for your environment.

## Base Resources Created

- [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- [Headless Service](https://kubernetes.io/docs/concepts/services-networking/service/#headless-services)
- [Certificate](https://cert-manager.io/docs/concepts/certificate/) - Issued by [cert-manager](https://cert-manager.io/docs/)
- [Ingress Gateway](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-control/)
- [Virtual Service](https://istio.io/latest/docs/reference/config/networking/virtual-service/)

## Environment Overlays

Environment specific resources are generated using [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/)

Once you run cookiecutter in create code from this template, you can run `kustomize build` in the overlays/dev or overlays/prod folders to see environment specific variants of the resources.

## Setup

- Follow the [Install Guide](https://cookiecutter.readthedocs.io/en/1.7.3/installation.html) based on your OS.

## Generating Code

- In a terminal window, navigate to a folder where you want to create a sub-folder for your application's state.

```bash
$ cookiecutter --directory web-deployment-istio-ingress https://github.com/bobmhong/k8s-cookiecutters.git
release_name [myapp]: 
system [myapp-system]: 
container_registry [default]: 
docker_image [nginx:1.23.4-alpine]: 
container_port [80]: 
expose_port [80]: 
health_path [/]: 
external_domain [example.com]: 
internal_domain [example]: 
min_replicas [1]: 
max_replicas [2]: 
max_cpu_percentage [80]: 
max_cpu [1024m]: 
max_memory [512Mi]: 
min_cpu [100m]: 
min_memory [128Mi]:

$ cd myapp
$ tree
.
└── k8s
    ├── base
    │   ├── certificate.yaml
    │   ├── deployment.yaml
    │   ├── hpa.yaml
    │   ├── ingress-gateway.yaml
    │   ├── kustomization.yaml
    │   ├── service.yaml
    │   └── virtual-service.yaml
    └── overlays
        ├── dev
        │   └── kustomization.yaml
        └── prod
            └── kustomization.yaml
```

### Parameters

The default paramters deploy a default nginx reverse proxy.

- `release_name` [myapp]: Application Name
- `system` [myapp-system]: Larger system that Application is part of (if any)
- `container_registry [default]: Use to prepend a private registry. e.g. mycompany.azurecr.io
- `docker_image` [nginx:1.23.4-alpine]: Image including tag
- `container_port` [80]: The port at which your container exposes service
- `expose_port` [80]: The port at which your service exposes the http port
- `health_path` [/]: The path used for health checks
- `external_domain` [example.com]: domain for external traffic
- `internal_domain` [example]: domain for internal traffic
- `min_replicas` [1]: Minimum number of pods to deploy.
- `max_replicas` [2]: Maximum number of pods that the autoscaler can spin up
- `max_cpu_percentage` [80]: CPU Percentage in Integer, Min: 0 - Max: 100. The HPA kicks in if CPU utilization crosses the threshold.
- `max_cpu` [1024m]: Maximum allowed CPU in Millicores a pod is allowed to consume
- `max_memory` [512Mi]: Maximum allowed Memory in megabytes a pod is allowed to consume
- `min_cpu` [100m]: Minimum CPU in Millicores required by the pod without which the pod will not run
- `min_memory` [128Mi]: Minimum Memory in megabytes required by the pod
