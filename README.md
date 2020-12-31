# Kubernetes Deployment for Ubuntu 20.04 (LTS) servers

This playbook: 
- Installs all necessary utilities to run kubernetes on an Ubuntu 20.04 server (docker, kube*, crio)
- Runs the necessary kubeadm commands to bootstap the cluster
- Deploys a pod network (Calico)
- Runs kubeadm commands on each kubenode to have the node join the cluster

**Disclaimer: This is by no means production ready, it was simply an exercise to teach myself [ansible](https://ansible.com).**

## Steps:

After creating an inventory file (inventory/yourcluster.yml) and populating the necessary values:

- controller_ip (IP for your kubernetes controller)

Run the playbook to get to the initial `kubeadm init` on the controller. 

`ansible-playbook playbook.yml -i inventory/linode-cluster.yml -vv` 

Take the generated join command from the controller, encrypt your token with ansible-vault (and your ca cert hash if you want), then run the play to have all kubenodes join the cluster. 

Next steps: Cleaning up the jobs to run in steps and eliminate extra/redundant operations.