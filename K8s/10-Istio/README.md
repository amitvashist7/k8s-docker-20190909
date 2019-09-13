# istio

## Kops configuration
```
kops edit cluster kubernetes.newtech.academy
```
Add:
```
  kubeAPIServer:
    admissionControl:
    - NamespaceLifecycle
    - LimitRanger
    - ServiceAccount
    - PersistentVolumeLabel
    - DefaultStorageClass
    - DefaultTolerationSeconds
    - MutatingAdmissionWebhook
    - ValidatingAdmissionWebhook
    - ResourceQuota
    - NodeRestriction
    - Priority
```

## download (1.0.2):
```
cd ~
wget https://github.com/istio/istio/releases/download/1.0.2/istio-1.0.2-linux.tar.gz
tar -xzvf istio-1.0.2-linux.tar.gz
cd istio-1.0.2
echo 'export PATH="$PATH:/youruserhomedir/istio-1.0.2/bin"' >> ~/.profile
```

``` 
Apply Cluster RoleBinding

kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin  --user=$(gcloud config get-value core/account)


```


```

```

## Istio install

Apply CRDs:

```
kubectl apply -f ~/istio-1.0.2/install/kubernetes/helm/istio/templates/crds.yaml
```

Wait a few seconds.


Option 1: with no mutual TLS authentication
```
kubectl apply -f ~/istio-1.0.2/install/kubernetes/istio-demo.yaml
```

Option 2: or with mutual TLS authentication
```
kubectl apply -f ~/istio-1.0.2/install/kubernetes/istio-demo-auth.yaml
```

## Example app

### Example app (from istio)
```
export PATH="$PATH:/home/ubuntu/istio-1.0.2/bin"
kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)
```

### Hello world app 
```
export PATH="$PATH:/home/ubuntu/istio-1.0.2/bin"
kubectl apply -f <(istioctl kube-inject -f helloworld.yaml)
kubectl apply -f helloworld-gw.yaml
```

### Mutual TLS example
Create pods, services, destinationrules, virtualservices
```
kubectl create -f <(istioctl kube-inject -f helloworld-tls.yaml)
kubectl create -f helloworld-legacy.yaml
```

### End-user authentication
```
kubectl create -f <(istioctl kube-inject -f helloworld-jwt.yaml)
kubectl create -f helloworld-jwt-enable.yaml
```
