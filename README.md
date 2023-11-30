# Knative routing project

For now repository contains:
* How to setup cluster tutorial
* Sample project from knative github

0. Good idea is to have Kubectx and Kubens installed to easly switch between clusters and namespaces. Not mandatory tho.
1. Create kind cluster:
```
cd setupCluster
kind create cluster --name mycluster --config kind-config.yaml 
```
2. Start setup script (remember to have the freshly created cluster context!), this may take a while because of broker.
```
./setup.sh
```
3. 