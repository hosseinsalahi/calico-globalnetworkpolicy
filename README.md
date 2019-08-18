# Calico Global Network Policy for k8s

## Minikube Setup 

```bash
minikube start \
 --extra-config=kubelet.network-plugin=cni \
 --extra-config=kubelet.pod-cidr=10.123.0.0/16 \
 --extra-config=controller-manager.allocate-node-cidrs=true \
 --extra-config=controller-manager.cluster-cidr=10.123.0.0/16 \
 --memory 8192
```

## Deploy Calico

```bash
kubectl create -f k8s-apps/calico.yaml
```

## Apply Initial Network Policies 

```bash
kubectl label namespaces kube-system name=kube-system
calicoctl create -f deny-all.yaml
calicoctl create -f allow-coredns.yaml
calicoctl create -f allow-dns-egress.yaml
calicoctl create -f allow-kube-system.yaml 
```

## Debug k8s Networking with Busybox
```bash
kubectl create -f k8s-apps/busybox.yaml
```
