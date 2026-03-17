---
weight: 10
title: "Gameserver"
description: "Gameserver Custom Resource Definition"
draft: false
---

# Gameserver

The `Gameserver` custom resource definition (CRD) represents a deployed game server instance in the PlayM8s platform. It defines the configuration and state of a running game server.

## Overview

A `Gameserver` resource specifies the game to run, the base configuration, and any overlays to apply. It also defines storage requirements and strategies for the game server.

## Example

```yaml
apiVersion: pm8s.io/v1
kind: Gameserver
metadata:
  name: my-csgo-server
spec:
  game: csgo
  gameserverBase: csgo-base
  gameserverOverlays:
    - csgo-overlay-config
    - csgo-overlay-maps
  storageClassName: fast-ssd
  storageStrategy: raw
```

## Specification

### Properties

- **game** (string, required): The game to deploy. Valid values are defined in the Games enum.
- **gameserverBase** (string, required): Reference to the GameserverBase resource to use as the foundation.
- **gameserverOverlays** (array of strings, optional): List of GameserverOverlay resources to apply to the base.
- **storageClassName** (string, required): The Kubernetes StorageClass to use for storing game files.
- **storageStrategy** (string, required): The storage strategy to use. Valid values are defined in the StorageStrategies enum.

### Enums

#### Games
- `csgo`: Counter-Strike: Global Offensive

#### StorageStrategies
- `raw`: Direct access to storage volumes
- `filesystem`: Filesystem-based access to storage

## Status

The status field contains information about the current state of the game server:

- **lastTransitionTime**: Timestamp of the last status change
- **message**: Human-readable status message
- **reason**: Programmatic reason for the status
- **observedGeneration**: The generation of the resource that was observed

## Usage

To create a Gameserver:

```bash
kubectl apply -f gameserver.yaml
```

To view running gameservers:

```bash
kubectl get gameservers
```