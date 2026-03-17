---
weight: 20
title: "GameserverBase"
description: "GameserverBase Custom Resource Definition"
draft: false
---

# GameserverBase

The `GameserverBase` custom resource definition (CRD) represents a base configuration for a game server. It defines the core files and settings needed to run a specific game, which can then be customized with GameserverOverlays.

## Overview

A `GameserverBase` resource contains the foundational files and configuration for a specific game. Multiple `Gameserver` instances can reference the same base, reducing storage requirements and simplifying management.

## Example

```yaml
apiVersion: pm8s.io/v1
kind: GameserverBase
metadata:
  name: csgo-base
spec:
  game: csgo
  storageClassName: fast-ssd
  storageStrategy: raw
```

## Specification

### Properties

- **game** (string, required): The game this base is for. Valid values are defined in the Games enum.
- **storageClassName** (string, required): The Kubernetes StorageClass to use for storing game files.
- **storageStrategy** (string, required): The storage strategy to use. Valid values are defined in the StorageStrategies enum.

### Enums

#### Games
- `csgo`: Counter-Strike: Global Offensive

#### StorageStrategies
- `raw`: Direct access to storage volumes
- `filesystem`: Filesystem-based access to storage

## Status

The status field contains information about the current state of the game server base:

- **lastTransitionTime**: Timestamp of the last status change
- **message**: Human-readable status message
- **reason**: Programmatic reason for the status
- **observedGeneration**: The generation of the resource that was observed

## Usage

To create a GameserverBase:

```bash
kubectl apply -f gameserverbase.yaml
```

To view available gameserverbases:

```bash
kubectl get gameserverbases
```