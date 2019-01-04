# kubernetes

## Installation

Before installing the virtualBox, need to enable couple of things:

### Disable secure boot:
#### Disable UEFI

 - Restart your system.
 - Click Troubleshoot → Advanced options → Start-up Settings → Restart.
 - Click repeatedly the F10/ Esc key (BIOS setup), before the “Startup Menu” opens.
 - Go to Boot Manager and disable the option Secure Boot.
   (https://github.com/tareque20/kubernetes/blob/master/secure-boot-disable.jpg)
 - Change the UEFI boot order according to the medium you want to boot the computer.
 - secure-boot-disable

 - Save the changes and reboot.

### Enable virtualization
 - While your PC is restarting repeatedly tap Esc key to enter BIOS
 - Press the F10 key for BIOS Setup.(Follow the instruction on the screen)
 - Press the right arrow key to System Configuration tab, Select Virtualization Technology and then press the Enter key. 
	(https://github.com/tareque20/kubernetes/blob/master/virt_bios.gif)
 - Select Enabled and press the Enter key.
 - Press the F10 key and select Yes and press the Enter key to save changes and Reboot.

### Installing VirtualBox
#### Update system
```sh
sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove && sudo apt-get install apt-transport-https
```
#### Install VirtualBox Hypervisor
```sh
sudo apt install virtualbox virtualbox-ext-pack
```
#### Download minikube
```sh
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```sh
chmod +x minikube-linux-amd64
```
```sh
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```
#### Version check
```sh
minikube version
minikube version: v0.28.0
```

### Install kubectl
```sh
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```
```sh
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
```sh
sudo apt update && sudo apt -y install kubectl
```

### Starting minikube
```sh
minikube start
```

> **Error:** Error restarting cluster: restarting kube-proxy: waiting for kube-proxy to be up for configmap update: timed out waiting for the condition.
```sh
minikube stop
```
```sh
minikube delete
```
```sh
minikube start
```


```sh
kubectl apply -f ./deployment.yaml
kubectl expose deployment tomcat-deployment --type=NodePort
minikube service tomcat-deployment --url
curl <URL>
```

### kubectl basic Commands
```sh
kubectl get pods
kubectl get pods [pod name]
 
kubectl expose <type name> <identifier/name> [—port=external port] [—target-port=container-port [—type=service-type]
kubectl expose deployment tomcat-deployment --type=NodePort
 
kubectl port-forward <pod name> [LOCAL_PORT:]REMOTE_PORT]
 
kubectl attach <pod name> -c <container>
 
kubectl exec  [-it] <pod name> [-c CONTAINER] — COMMAND [args…]
kubectl exec -it <pod name> bash
 
kubectl label [—overwrite] <type> KEY_1=VAL_1 ….
kubectl label pods <pod name> healthy=fasle
 
kubectl run <name> —image=image
kubectl run hazelcast --image=hazelcast/hazelcast --port=5701
# the hazelcast docker image has been moved to hazelcast/hazelcast (https://hub.docker.com/r/hazelcast/hazelcast
 
kubectl describe pod
```

