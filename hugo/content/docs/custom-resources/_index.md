---
weight: 500
title: "Custom Resources"
description: "PlayM8s Custom Resource Definitions"
draft: false
---

# Custom Resources

PlayM8s uses several Custom Resource Definitions (CRDs) to manage game servers on Kubernetes. These resources work together to provide a flexible and efficient way to deploy and manage game servers.

## Core Resources

### Gameserver
The `Gameserver`](gameserver/) resource represents a deployed game server instance. It defines the configuration and state of a running game server, including which base and overlays to use.

### GameserverBase
The [`GameserverBase`](gameserverbase/) resource contains the foundational files and configuration for a specific game. Multiple Gameserver instances can reference the same base, reducing storage requirements.

### GameserverOverlay
The [`GameserverOverlay`](gameserveroverlay/) resource contains additional files and configurations that can be overlaid on top of a GameserverBase to customize game server instances.

## Relationship Between Resources

``mermaid
graph TD
    A[GameserverBase] --> B[Gameserver]
    C[GameserverOverlay] --> B
```

A `Gameserver` combines one `GameserverBase` with zero or more `GameserverOverlays` to create a complete game server deployment. The base provides the core game files, while overlays provide customizations such as configuration files, maps, or mods.

## Usage Pattern

1. Create a `GameserverBase` with the core game files
2. Create `GameserverOverlays` for different configurations or customizations
3. Deploy `Gameserver` instances referencing the base and any desired overlays

This approach allows for efficient storage and management of multiple game server instances with shared base files but different customizations.