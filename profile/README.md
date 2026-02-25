# PlayM8s

> PlayM8s, a gameserver's best friend

## What is PlayM8s?

PlayM8s (PM8s) is an ecosystem of tooling to help manage the lifecycle of various gameservers \
in a kubernetes cluster.

> PlayM8s is currently a WIP and is undergoing heavy development. \
> Keep an eye on releases, we're getting towards a `1.0.0` soon! \
> Until then, feel free to follow along, but let it be known that there be dragons here.

---

## Helpful Links

| **Link**
| ---
| [**Homepage**](https://pm8s.io)
| [**Documentation**](https://pm8s.io/docs)
| [**Helm Repo**](https://helm.pm8s.io) ([***Git Repo***](https://github.com/playm8s/helm))
| [**Operator**](https://github.com/playm8s/operator)
| [**CRDs**](https://github.com/playm8s/crds)

---

## Requirements

PlayM8s should run on any normal k8s distribution, however some features depend on [Cilium](https://cilium.io/) and [Multus](https://github.com/k8snetworkplumbingwg/multus-cni)
being the CNIs in the cluster.

[RKE2](https://docs.rke2.io/) is recommended.

### Development architecture (the "home" setup)

- 1x 4c/8g VM
  - Ubuntu 24.04 w/ HWE kernel
  - RKE2 for k8s
  - Cilium and Multus as the CNIs
  - Network interface in L2 domain usable by Cilium for [L2 Announcements](https://docs.cilium.io/en/latest/network/l2-announcements/)
  - [Local-Path-Provisioner](https://github.com/rancher/local-path-provisioner) for provisioning storage local to the host

### Production architecture (the "cloud" setup)

- 3x 4c/8g VMs
  - Ubuntu 24.04 w/ HWE kernel
  - RKE2 for k8s
  - Cilium and Multus as the CNIs
  - A provider that supports announcing IPs with BGP via Cilium [BGP Control Plane](https://docs.cilium.io/en/latest/network/bgp-control-plane/bgp-control-plane/#bgp-control-plane) and [LoadBalancer IP Address Management](https://docs.cilium.io/en/latest/network/lb-ipam/) is preferred
    - Cilium [Node IPAM LB](https://docs.cilium.io/en/latest/network/node-ipam/) or similar can be used if this is not possible
  - [Local-Path-Provisioner](https://github.com/rancher/local-path-provisioner) for provisioning storage local to the host, or more ideally from a shared filesystem

---

## Getting Started

### Deploying the PM8s CRDs

The only supported method of deploying the PM8s CRDs is with Helm.

Management with FluxCD is recommended.

Helm repo is at [https://helm.pm8s.io/](https://helm.pm8s.io/)

Manually install with helm cli:

```bash
helm repo add pm8s https://helm.pm8s.io
helm repo update

helm install pm8s-crds pm8s/crds
```

### Deploying the PM8s Operator

The only supported method of deploying the PM8s Operator is with Helm.

Management with FluxCD is recommended.

Helm repo is at [https://helm.pm8s.io/](https://helm.pm8s.io/)

Manually install with helm cli:

```bash
helm repo add pm8s https://helm.pm8s.io
helm repo update

helm install pm8s-operator pm8s/operator
```

### Deploying your first gameserver

Stay tuned!
