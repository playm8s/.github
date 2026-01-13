---
weight: 2
title: "Quickstart"
description: "Start here!"
draft: false
toc: true
---

> PlayM8s, a gameserver's best friend

## What is PlayM8s?

PlayM8s (pm8s) is an ecosystem of tooling to help manage the lifecycle of various gameservers \
in a kubernetes cluster.

> PlayM8s is currently a WIP and is undergoing heavy development
> Keep an eye on releases, we're getting towards a `1.0.0` soon!

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

PlayM8s should run on any normal k8s distribution.

The reference architecture is 3x 4c/8g VMs running RKE2 with Cilium as the CNI and a shared filesystem for the CSI

---

## Getting Started

### Deploying the pm8s CRDs

Currently the only supported method of deploying the pm8s CRDs is with kubectl.

Check the [latest release in the crds repo](https://github.com/playm8s/crds/releases/latest) for yaml definitions.

### Deploying the pm8s Operator

Currently the only supported method of deploying the pm8s Operator is with Helm.

See the [gh-pages](https://github.com/playm8s/helm/blob/gh-pages/charts/operator/values.yaml) branch of the Helm repo for details.

### Deploying your first gameserver

Stay tuned!
