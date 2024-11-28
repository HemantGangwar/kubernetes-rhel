![image](https://user-images.githubusercontent.com/38517925/86527948-5f983e80-bec1-11ea-9be7-03a6cc7792c8.png)

# Kubernetes Deployment Role

## Overview

This Ansible role simplifies the deployment of Kubernetes clusters by automating the setup of master and worker nodes, CRI-O installation, and essential pre- and post-deployment validation. It ensures a streamlined, repeatable process for Kubernetes installations across multiple environments.

![image](https://user-images.githubusercontent.com/38517925/86524357-5abe9500-be97-11ea-8f15-d997b4ce7d3e.png)

## Features

1. 🚀 **Automated Kubernetes Deployment**: Deploys Kubernetes control plane and worker nodes seamlessly.\
2. ✅ **Pre- and Post-deployment Checks**: Validates environment readiness and cluster health.\
3. 🛠️ **Customizable**: Execute specific tasks using tags for flexibility.\
4. 🔒 **CRI-O Installation**: Configures CRI-O as the container runtime.

## Requirements

### Supported Platforms:
> Red Hat Enterprise Linux 8, 9\
> CentOS 8, 9\
> Minimum of 2 CPU and 2 GB of RAM

### Software Requirements:
> Ansible 2.9+\
> Python installed on all target nodes\
> Selinux module loaded from collections.

### Permissions:
> sudo access is required on all target nodes.

## Structure

![image](https://github.com/user-attachments/assets/5912f5c4-50aa-4b22-86b4-2bedc331b6bc)


## Installation

- ### Clone this repository:

> git clone https://github.com/yourusername/kubernetes-deployment-role.git \
> cd kubernetes-deployment-role

- ### Usage
Example Playbook

Create a playbook to invoke this role from Ansible **Control Node**:

        - name: Deploy Kubernetes Cluster
          hosts: all
          become: true
          vars_prompt:
            - name: KUBERNETES_MASTER
              prompt: "Enter the FQDN of your Kubernetes Master Node"
              private: false
          roles:
            - kubSetup

Same playbook invoked from **Tower**:

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
always | Logs the start and end of the deployment process.

### Run specific tags:

> ansible-playbook kubernetes_ansible_playbook.yml --tags "validation,install"

## Variables Used

Variable Name | Type | Details
|-------------|------|--------|
KUBERNETES_MASTER | Prompt Variable | This will be holding the node fqdn which will be act as kubernetes master.
kubernetes_master_name | Custom Fact | This will be holding the node fqdn which will be act as kubernetes master.
FIREWALL_PORTS | Role Variable | This is an array of Firewall ports which need to be allowed. 
netfilermodule | Register | Holding count of modules found for required installation
SYSCTL_NF_CALL_RULES | Role Variable | Kernel network rules.
crio_pkg | Role Variable | Container runtime cri-o package.
crio_svc | Role Variable | Crio service name
KUBERNETES_PACKAGES | Role Variable | Array of packages required for kubernetes installation.
KUBELET_SERVICE | Role Variable | Kubelet service name
API_SERVER_IP | Role Variable | IPv4 address of API
INTERNAL_POD_NETWORK | Role Variable | Network segment for pods
kubeadmin_init | Register | Register holding kubernetes initialization results
joinWorkerNodes | Register | Join commands to be used by worker nodes
NETWORK_TIME_WAIT | Role Variable | Wait time before networking setup
CALICO_PATH | Role Variable | Calco url for networking
VERIFICATION_TIME_WAIT | Role Variable | Wait time before Verifications
kubectl_nodes | Register | Kubernetes cluster node information
kubectl_pods | Register | Kubernetes cluster pods information






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
Feel free to reach out at your.email@example.com or connect on LinkedIn.

This README.md is designed for GitHub with proper formatting, badges, and links. Let me know if you'd like to add any specific sections!
