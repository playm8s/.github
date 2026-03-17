---
weight: 1
title: "Docs Home"
description: "Welcome to pm8s.io"
draft: false
---

# Welcome to PlayM8s Documentation

PlayM8s (PM8s) is an ecosystem of tooling designed to help manage the lifecycle of various game servers in a Kubernetes cluster.

Whether you're running a small home setup or a large-scale cloud deployment, PlayM8s provides the tools you need to efficiently deploy, manage, and scale game servers.

## Core Components

### Custom Resource Definitions (CRDs)
PlayM8s introduces three custom resource definitions that work together to manage game servers:
- [Gameserver](custom-resources/gameserver/): Represents a deployed game server instance
- [GameserverBase](custom-resources/gameserverbase/): Contains the foundational files for a specific game
- [GameserverOverlay](custom-resources/gameserveroverlay/): Provides customizable overlays for game server instances

### Operator
The [PlayM8s Operator](operator/) manages the lifecycle of game servers, handling deployment, scaling, and maintenance tasks. It watches for changes to the custom resources and ensures that the actual state of the cluster matches the desired state.

### Helm Charts
Helm charts provide an easy way to deploy PlayM8s components and game servers.

## Getting Started

If you're new to PlayM8s, start with our [Quickstart Guide](quickstart/) to get up and running quickly.

## Architecture Overview

PlayM8s uses a composable architecture where game servers are built from a base configuration plus optional overlays. This approach allows for efficient storage usage while maintaining flexibility for customization.

For detailed information about each component, see the respective documentation sections.