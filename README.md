# Calico Global network Policy for K8s

## Minikube setup 

```bash
minikube start \
 --extra-config=kubelet.network-plugin=cni \
 --extra-config=kubelet.pod-cidr=10.123.0.0/16 \
 --extra-config=controller-manager.allocate-node-cidrs=true \
 --extra-config=controller-manager.cluster-cidr=10.123.0.0/16 \
 --memofry 819
```

## Deploy Calico

```bash
kubectl create -f k8s-apps/calico.yaml
```

## Apply initial network policies 

```bash
calicoctl create -f deny-all.yaml
calicoctl create -f allow-coredns.yaml
calicoctl create -f allow-dns-egress.yaml
calicoctl create -f allow-kube-system.yaml 
```
