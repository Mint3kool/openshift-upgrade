# Purpose

This repository makes use of Ansible scripts use to upgrade Openshift Clusters using the Cluster Version Operator built in Openshift. Be aware that this repo is a work in progress, and may break clusters upon use.

Some resources based off of https://github.com/sushilsuresh/ocp4-ansible-roles

# Background

The OpenShift Container Platform allows users to upgrade their clusters. The Cluster Version Operator (CVO) built into the platform allows a user to determine the safe upgrade paths for your cluster, and the current upgrade status of the cluster. During an upgrade process, the Machine Config Operator (MCO) will apply the upgrade configurations to your machines.

More information on the upgrade process, and how it works: https://docs.openshift.com/container-platform/4.3/updating/updating-cluster-between-minor.html

Cluster Version Operator Source Code: https://github.com/openshift/cluster-version-operator

# Architecture

Information about these scripts:
* Openshift 4.3.X on VMware 6.7
* Ansible 2.9.9
* Run logged into the openshift cluster as localhost from personal machine

# Assumptions

* Your user has access to the cluster with admin privileges
* You have a recent backup of the cluster in case the upgrade process fails

# Solution

1. Pre Upgrade
    * Verifys that the cluster is up
    * Checks current cluster operator health
    * Checks current cluster status
2. Gathering Cluster Information
    * Gets the current upgrade paths and displays them to the user
3. Upgrading The Cluster
    * Runs
    > oc adm upgrade --to=<cluster_version>
4. Post Upgrade
    * Makes sure the cluster is up
    * Makes sure all cluster operators are up
