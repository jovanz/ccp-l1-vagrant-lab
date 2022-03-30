# ccp-l1-vagrant-lab
Certified Calico Operator: Level 1 lab setup with Vagrant and Ansible on Ubuntu 18.04 LTS 

## Install Kubernetes 

To install kubernetes run ansible playbook:
```bash
ansible-playbook install-kubernetes-playbook.yaml
```
and to create new cluster and set up on worker nodes run next two ansible playbook in this order:
```bash
ansible-playbook setting-up-kubernetes-cluster-master-playbook.yaml
ansible-playbook setting-up-kubernetes-cluster-worker-playbook.yaml
```

After this to verify that is all install run:
```bash
vagrant ssh k8s-master
```
and inside VM run:
```bash
kubectl get nodes -o wide
```
Output shoud be:
![kubernetes-vagrant-cluster](https://user-images.githubusercontent.com/7665799/130684017-1351db07-9b46-4306-88fe-644f4a746746.png)

This is entry point for CCO-L1 lab.

We will be using the Tigera Operator to install and configure Calico.
```bash
wget https://docs.projectcalico.org/archive/v3.22/manifests/tigera-operator.yaml
kubectl create -f tigera-operator.yaml
```
and after this run:
```bash
cat <<EOF | kubectl apply -f -
apiVersion: operator.tigera.io/v1
kind: Installation
metadata:
  name: default
spec:
  calicoNetwork:
    containerIPForwarding: Enabled
    ipPools:
    - cidr: 192.168.56.0/21
      natOutgoing: Enabled
      encapsulation: None
EOF
```
