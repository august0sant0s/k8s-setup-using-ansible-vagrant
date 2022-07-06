# k8s-setup-using-ansible-vagrant
It's a setup based on [kubernetes-setup-using-ansible-and-vagrant](https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/) Kubernetes blog's post by Naresh L J (Infosys).

## Improvements:
- using crio;
- parallel execution during setup nodes;
- k8s version choose;
- shared folder host/vm; 

If you intend to use shared folder, please install:
```vagrant plugin install vagrant-vbguest```
or just comment the line.

### To begin
- Clone this repo;
- Install vagrant cli;
- Edit Vagrant file and ajust your VMs size
- run: ```vagrant up```
- to connect ```vagrant ssh k8s-master```
