# Azure

# Install Azure CLI 2.0

- Linux

On Linux, you may need to install specific prerequisites.

Install Azure CLI 2.0 with one curl command.

- curl -L https://aka.ms/InstallAzureCli | bash

You may have to restart your command shell for some changes to take effect.

- exec -l $SHELL

Run Azure CLI 2.0 from the command prompt with the az command.

# Create an SSH public and private key pair for Linux VMs

Run the following commands from a Bash shell, replacing the examples with your own choices.

SSH keys are by default kept in the ~/.ssh directory. If you do not have a ~/.ssh directory, the ssh-keygen command creates it for you with the correct permissions. The -N argument specifies the password to encrypt the private SSH key and is not your user password.

- ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -N mypassword

Add the newly created key to ssh-agent:

-  ssh-add ~/.ssh/id_rsa

# Create your Kubernetes cluster

Create a resource group

To create your cluster, you first need to create a resource group in a specific location. Run commands similar to the following:

- RESOURCE_GROUP=my-resource-group
- LOCATION=westus
- az group create --name=$RESOURCE_GROUP --location=$LOCATION

Create a cluster

Once you have a resource group, you can create a cluster in that group:

- DNS_PREFIX=some-unique-value
- CLUSTER_NAME=any-acs-cluster-name
- az acs create --orchestrator-type=kubernetes --resource-group $RESOURCE_GROUP --name=$CLUSTER_NAME --dns-prefix=$DNS_PREFIX

Note

During deployment, the CLI uploads ~/.ssh/id_rsa.pub to the Linux VMs.2

Once that command is complete, you should have a working Kubernetes cluster.

Connect to the cluster

Following are Azure CLI commands to connect to the Kubernetes cluster from your client computer by using kubectl, the Kubernetes command-line client. For more information, see Connect to an Azure Container Service cluster.

If you don't already have kubectl installed, you can install it with:

-az acs kubernetes install-cli

Once kubectl is installed, run the following command to download the master Kubernetes cluster configuration to the ~/.kube/config file:3

- az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME

At this point you should be ready to access your cluster from your machine. Try running:

- kubectl get nodes

Verify that you can see a list of the machines in your cluster.
