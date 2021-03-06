# kubench ![Shellcheck](https://github.com/vincentserpoul/kubench/workflows/Shellcheck/badge.svg?branch=master)

# Goal

Benchmark different containerized applications within a kubernetes cluster.

## Pre-requisites

- [k3d v3](https://github.com/rancher/k3d)
- [kubectl v1.17.3](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [helm v3](https://helm.sh/docs/intro/install/)
- [doctl v1.43.0](https://github.com/digitalocean/doctl) - if you re running in digitalocean

## Cluster management

```bash
    ./cluster.sh --help
```

You can create a cluster with:

- k3d, locally (default, or with -p k3d)
- digital ocean managed k8s (requires doctl and a digital ocean account) (with -p digitalocean)

## Benches

### Raw HTTP GET

to run locally

```bash
    ./cluster.sh
    ./benches/raw-http-get/bench.sh
    ./cluster.sh -a delete -p k3d
```

to run in k8s digital ocean

```bash
    ./cluster.sh -p digitalocean
    ./benches/raw-http-get/bench.sh
    ./cluster.sh -a delete -p digitalocean
```

results should appear in ./benches/raw-http-get/

### REST

<!-- TODO -->

### Databases

<!-- TODO -->

## Using your own docker namespace

You can re-build all images by running:

```bash
./applications/build-n-push.sh <YOUR_BASE_DOCKER_REPO>
```

You will also need to rebuild the bencher

```bash
docker build ./bencher/ --rm -t <YOUR_BASE_DOCKER_REPO>/kubench-bencher -f ./bencher/Dockerfile
docker push <YOUR_BASE_DOCKER_REPO>/kubench-bencher
```

Then, you should be able to launch the benches with your own images:

```bash
./benches/raw-http-get/bench.sh <YOUR_BASE_DOCKER_REPO>
```

## To do list

- [ ] Add github actions to auto build containers
