## Scaling Pods in Kubernetes


### Initialize cluster
```sh
kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=v1.11.3

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Add other nodes
```sh
kubeadmin join <IP ADDRESS>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASHED TOKEN>
```

### Install Flannel on master
```sh
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.9.1/Documentation/kube-flannel.yml
```
Run
```sh
kubectl get nodes
```


### After deployment file
```sh
kubectl create -f deployment.yml
kubectl get pods
```

### After creating service file
```sh
kubectl create -f service.yml
kubectl get services
```

### Scale deployment up and down

In order to scale the number of replicas up or down, we need only edit deployment.yml. Change the replicas: line from 3 to 5, then apply the changes:

```sh
kubectl apply -f deployment.yml
```
Now if we check with `kubectl get pods`, we'll see there are five. But what if five is too many?


