# k8s-cookiecutters

This repository contains templates for generating Kubernetes manifests using [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html).

By using Cookiecutter, you'll be prompted to enter values for your application, but can accept sensible default values.

For more control, you can create a [User Config](https://cookiecutter.readthedocs.io/en/stable/advanced/user_config.html) file to pre-populate settings suitable for your environment.

## Setup

- Follow the [Install Guide](https://cookiecutter.readthedocs.io/en/stable/installation.html) based on your OS.

## Example

This example generates code for the cookiecutter in the web-deployment-istio-ingress directory.

- In a terminal window, navigate to a folder where you want to create a sub-folder for your application's state.
- hit enter for each prompt to accept the defaults.

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

For more details on each chart, see the [README.md](./web-deployment-istio-ingress/README.md) file within each template directory.

You may also want to visit [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/README.html) to learn about advanced configuration or to create your own templates.