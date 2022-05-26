# Deploying Sourcegraph to Kubernetes (k8s) without Helm

## Introduction
This material is intended to be used as a handout to customers working with a Sourcegraph Customer Engineer to deploy their own instance. The materials are meant to serve as an overview and resource to aid in deep diving into Sourcegraph's documentation and common deployment tasks.

**Table of Contents:**

- [Introduction](#introduction)
- [Sourcegraph Setup and Deployment](#sourcegraph-setup-and-deployment)
	- [Prerequisites](#prerequisites)
  - [Create your cluster](#create-your-cluster)
  - [Configure your manifest file](#configure-your-manifest-file)
  - [Install Sourcegraph](#install-sourcegraph)
- [Next Steps](#next-steps)

## Sourcegraph Setup and Deployment

### Prerequisites
- Ensure you have your Sourcegraph Enterprise License
- Access to deploy Kubernetes clusters
  - Minimum Kubernetes version: `v1.19` and `kubectl` `v1.19`
  - Support for Persistent Volumes (SSDs strongly recommended)
- Determine resource requirements to properly size your instance: [Resource Estimator](https://docs.sourcegraph.com/admin/deploy/resource_estimator)
- Install relevant CLIs for your provider of choice:
  - AWS: [`aws` cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and [`ejsctk`](https://eksctl.io/introduction/#installation)
  - Azure: [`az` cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
  - GCP: [`gcloud` cli](https://cloud.google.com/sdk/gcloud)

### Create your cluster
- Follow the instructions for your provider of choice to create your Kubernetes (k8s) cluster: [Cloud installation instructions](https://docs.sourcegraph.com/admin/deploy/kubernetes#cloud-installation)
  - Follow the recommendations for `node type`, `disk type`, and `minimum` and `maximum` nodes

### Configure your manifest file
Sourcegraph has a list of configurations available and recommended that need to be made to your manifest file to properly install Sourcegraph into your cluster. Please review the full configuration guide prior to proceeding: [Configure Sourcegraph with Kubernetes](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure)

Get started by following these steps to fork the [`deploy-sourcegraph`](https://github.com/sourcegraph/deploy-sourcegraph) repository: [Getting started](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#getting-started)

- Configurations:
  - [License Key](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#add-license-key)
  - [Storage Class](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#configure-a-storage-class)
  - [Network Access](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#configure-network-access)
  - [External PostgreSQL Database](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#sourcegraph-databases)
  - [Scaling for services](https://docs.sourcegraph.com/admin/deploy/kubernetes/scale#tuning-replica-counts-for-horizontal-scalability)
  - [Cluster role administrator access](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

### Install Sourcegraph
With your manifest file configured, ensure that you can [access your cluster](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/) with `kubectl` and `kubectl` is pointed to the proper context.

- Follow the [Direct installation](https://docs.sourcegraph.com/admin/deploy/kubernetes#direct-installation) steps to apply your manifest to your cluster
- Once your deployment is completed, you can access Sourcegraph via the [ingress](https://docs.sourcegraph.com/admin/deploy/kubernetes/configure#ingress-controller-recommended) you configured in your manifest

## Next steps
Congratulations, Sourcegraph is now deployed and you can begin to configure your instance. We recommend you review the [Configurating Sourcegraph](https://docs.sourcegraph.com/admin/config) documentation next to [add a code host](https://docs.sourcegraph.com/admin/external_service), [configure SSO](https://docs.sourcegraph.com/admin/auth), and more.
