# Kubernetes Deployment Role

## Overview

This Ansible role simplifies the deployment of Kubernetes clusters by automating the setup of master and worker nodes, CRI-O installation, and essential pre- and post-deployment validation. It ensures a streamlined, repeatable process for Kubernetes installations across multiple environments.

## Features

1. 🚀 Automated Kubernetes Deployment: Deploys Kubernetes control plane and worker nodes seamlessly.\
2. ✅ Pre- and Post-deployment Checks: Validates environment readiness and cluster health.\
3. 🛠️ Customizable: Execute specific tasks using tags for flexibility.\
4. 🔒 CRI-O Installation: Configures CRI-O as the container runtime.

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

## Installation

- ### Clone this repository:

> git clone https://github.com/yourusername/kubernetes-deployment-role.git \
> cd kubernetes-deployment-role

- ### Usage
Example Playbook

Create a playbook to invoke this role:

        - name: Deploy Kubernetes Cluster
          hosts: all
          become: true
          vars_prompt:
            - name: KUBERNETES_MASTER
              prompt: "Enter the FQDN of your Kubernetes Master Node"
              private: false
          roles:
            - kubSetup

Same playbook invoked from Tower:

        - name: Deploy Kubernetes Cluster
          hosts: all
          become: true
          roles:
            - kubSetup

- ### Run the playbook:

> ansible-playbook kubernetes_ansible_playbook.yml

## Tags

Tag Name | Description
|--------|------------|
validation | Pre-deployment validation tasks.
setup | General setup tasks for the cluster.
install | Installation tasks for CRI-O and Kubernetes.
master | Tasks specific to Kubernetes Master node setup.
worker | Tasks specific to Kubernetes Worker node setup.
deployment | Deployment-related tasks for cluster nodes.
post-deployment | Validation and cleanup tasks after cluster deployment.

### Run specific tags:

> ansible-playbook kubernetes_ansible_playbook.yml --tags "validation,install"

## Task Workflow

Sr|Task|Description
|-|----|-----------|
1 | Pre-deployment Validation | Checks for environment readiness, such as OS version and required packages.
2 | Common Setup | Installs dependencies and common configurations.
3 | CRI-O Installation | Installs CRI-O as the container runtime.
4 | Kubernetes Installation | Deploys the Kubernetes control plane.
5 | Master Node Configuration | Configures the Kubernetes Master node and generates the join command for workers.
6 | Worker Node Configuration | Applies the join command to configure worker nodes.
7 | Post-deployment Validation | Performs cluster health checks and validation.

## Contributing

We welcome contributions!

    Fork the repository.
    Create a feature branch.
    Submit a pull request with your changes.

For significant changes, please open an issue to discuss your proposal.
## License

This project is licensed under the MIT License.
## Author

  Hemant Gangwar
Linux and Kubernetes Administrator
Feel free to reach out at your.email@example.com or connect on LinkedIn.

This README.md is designed for GitHub with proper formatting, badges, and links. Let me know if you'd like to add any specific sections!
