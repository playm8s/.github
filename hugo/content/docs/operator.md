---
weight: 400
title: "Operator"
description: "PlayM8s Operator Documentation"
draft: false
---

# Operator

The PlayM8s Operator is a Kubernetes operator that manages the lifecycle of game servers and their associated resources. It watches for changes to Custom Resources (CRs) and ensures that the actual state of the cluster matches the desired state defined in those resources.

## Overview

The operator is responsible for:

1. Watching for changes to Gameserver, GameserverBase, and GameserverOverlay resources
2. Reconciling the state of these resources with Kubernetes deployments
3. Managing the creation, updating, and deletion of game server deployments

## Managed Resources

### Gameserver

When a Gameserver resource is created, modified, or deleted, the operator:

- Creates a corresponding Kubernetes Deployment with the appropriate configuration
- Sets environment variables for the game server container based on the Gameserver spec
- Manages the lifecycle of the deployment, ensuring it matches the desired state
- Deletes the deployment when the Gameserver resource is deleted

### GameserverBase

The operator watches for GameserverBase resources, though it currently doesn't create deployments for them. GameserverBase resources serve as templates that can be referenced by Gameserver resources.

### GameserverOverlay

Similar to GameserverBase, the operator watches for GameserverOverlay resources but doesn't create deployments for them. These resources provide customizable layers that can be applied to Gameserver instances.

## Environment Variables

The operator sets the following environment variables in the game server containers:

- `NAMESPACE`: The namespace where the Gameserver resource is deployed
- `RESOURCE_NAME`: The name of the Gameserver resource
- `GAME`: The game specified in the Gameserver spec
- `GAMESERVER_BASE`: The GameserverBase reference from the spec
- `STORAGE_CLASS_NAME`: The storage class name from the spec

## Configuration

The operator can be configured using the following environment variables:

- `NAMESPACE`: The namespace the operator should watch (default: "pm8s-system")
- `WATCH_OTHER_NAMESPACES`: Whether the operator should watch namespaces other than its own (default: "false")
- `KUBE_IN_CLUSTER_CONFIG`: Whether to use in-cluster Kubernetes configuration (default: parsed from environment)

## API Endpoints

The operator exposes a simple HTTP API with the following endpoints:

- `GET /`: Health check endpoint that returns basic information about the operator
- `GET /api/*`: Various API endpoints for managing and monitoring the operator

## Metrics

The operator collects and exposes metrics about resource events and active watches, which can be used for monitoring and alerting.

## Deployment

The operator is typically deployed using the official Helm chart:

```bash
helm repo add pm8s https://helm.pm8s.io
helm repo update
helm install pm8s-operator pm8s/operator
```