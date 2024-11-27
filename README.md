# Kubernetes Deployment Role

## Overview

This Ansible role simplifies the deployment of Kubernetes clusters by automating the setup of master and worker nodes, CRI-O installation, and essential pre- and post-deployment validation. It ensures a streamlined, repeatable process for Kubernetes installations across multiple environments.

## Features


1. Automated Kubernetes Deployment: Deploys Kubernetes control plane and worker nodes seamlessly.\
2. Pre- and Post-deployment Checks: Validates environment readiness and cluster health.\
3. Customizable: Execute specific tasks using tags for flexibility.\
4. CRI-O Installation: Configures CRI-O as the container runtime.

## Requirements

### Supported Platforms:
> Red Hat Enterprise Linux 8, 9\
> CentOS 8, 9

### Software Requirements:
> Ansible 2.9+\
> Python installed on all target nodes\
> Selinux module loaded from collections.

### Permissions:
> sudo access is required on all target nodes.
