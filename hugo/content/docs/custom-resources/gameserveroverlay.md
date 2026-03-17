---
weight: 30
title: "GameserverOverlay"
description: "GameserverOverlay Custom Resource Definition"
draft: false
---

# GameserverOverlay

The `GameserverOverlay` custom resource definition (CRD) represents a set of files and configurations that can be overlaid on top of a GameserverBase to customize a game server instance.

## Overview

A `GameserverOverlay` resource contains additional files, configurations, or modifications that can be applied to a GameserverBase. This allows for customization of game servers without duplicating the base files, enabling efficient storage and management.

## Example

```yaml
apiVersion: pm8s.io/v1
kind: GameserverOverlay
metadata:
  name: csgo-overlay-config
spec:
  game: csgo
  storageClassName: fast-ssd
  storageStrategy: raw
```

## Specification

### Properties

- **game** (string, required): The game this overlay is for. Must match the game of the GameserverBase it will be applied to.
- **storageClassName** (string, required): The Kubernetes StorageClass to use for storing overlay files.
- **storageStrategy** (string, required): The storage strategy to use. Valid values are defined in the StorageStrategies enum.

### Enums

#### Games
- `csgo`: Counter-Strike: Global Offensive

#### StorageStrategies
- `raw`: Direct access to storage volumes
- `filesystem`: Filesystem-based access to storage

## Status

The status field contains information about the current state of the game server overlay:

- **lastTransitionTime**: Timestamp of the last status change
- **message**: Human-readable status message
- **reason**: Programmatic reason for the status
- **observedGeneration**: The generation of the resource that was observed

## Usage

To create a GameserverOverlay:

```bash
kubectl apply -f gameserveroverlay.yaml
```

To view available gameserveroverlays:

```bash
kubectl get gameserveroverlays
```

To use overlays with a Gameserver, reference them in the Gameserver specification:

```yaml
apiVersion: pm8s.io/v1
kind: Gameserver
metadata:
  name: my-custom-csgo-server
spec:
  game: csgo
  gameserverBase: csgo-base
  gameserverOverlays:
    - csgo-overlay-config
    - csgo-overlay-maps
  storageClassName: fast-ssd
  storageStrategy: raw
```