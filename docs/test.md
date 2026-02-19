# Actual Progress

We have tested following:

## Tested Steps

- On vyl-hpe.eecs.umich.edu
- create three Ubuntu 24.04 LTS VMs: ```k0, k1, k2```
- We are not exactly following the [exact commands in index.html](https://um-cse-k8s.github.io/index.html) but the most of the steps are similar.  So see details below.

## Step 1-4
- Medium article on [How to Install Kubernetes Cluster on Ubuntu 24.04 LTS (Step-by-Step Guide)] P() and its [PDF](./How_to_Install_K8s.pdf).

- A better Medium article on [](https://medium.com/@osama.abusitta/step-by-step-building-a-kubernetes-cluster-from-scratch-on-ubuntu-24-04-2025-guide-822452f14dab)
- To remove kubernetes installation, see [this page](kubectl drain <node-name> --delete-emptydir-data --force --ignore-daemonsets and kubectl delete node <node-name>)
- When CNI does not work, debug it with [these hints](https://www.google.com/search?q=after+install+kubernetes+on+master+node%2C+the+node+is+NotReady&oq=after+install+kubernetes+on+master+node%2C+the+node+is+NotReady&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRiPAtIBCTExMjAyajBqN6gCALACAA&sourceid=chrome&ie=UTF-8)
- For missing CNI, if Calico, use a command in the comment by Michael as ```kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml```
- For missing CNI, use cilium with [how to install cilium CNI for kubernetes](https://www.google.com/search?q=how+to+install+cilium+CNI+for+kubernetes&oq=how+to+install+cilium+CNI+for+kubernetes&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigATIHCAMQIRigATIHCAQQIRigATIHCAUQIRigAdIBBzE0OWowajeoAgCwAgA&sourceid=chrome&ie=UTF-8)
- Here is [a comparison of Calico and Cilium](https://www.google.com/search?q=compare+K8S+CNI+between+calico+and+cilium&sca_esv=9447ce1ae06b4598&sxsrf=ANbL-n7pXpn4nkNgU9kstLGxQGJmukD1Lw%3A1770506579834&ei=U8mHaYe7Mqu5p84P6NnG-Q8&biw=1204&bih=713&ved=0ahUKEwjHsI3-wsiSAxWr3MkDHeisMf8Q4dUDCBM&uact=5&oq=compare+K8S+CNI+between+calico+and+cilium&gs_lp=Egxnd3Mtd2l6LXNlcnAiKWNvbXBhcmUgSzhTIENOSSBiZXR3ZWVuIGNhbGljbyBhbmQgY2lsaXVtMgUQABjvBTIFEAAY7wUyCBAAGKIEGIkFMgUQABjvBTIIEAAYgAQYogRItEVQxx1Yz0BwAngBkAEAmAFtoAHrCqoBBDE0LjK4AQPIAQD4AQGYAhKgAsYLwgIKEAAYsAMY1gQYR8ICBBAhGAqYAwCIBgGQBgiSBwQxNC40oAfvO7IHBDEyLjS4B78LwgcGMS4xMS42yAcwgAgA&sclient=gws-wiz-serp)
- [Install Helm](https://helm.sh/docs/intro/install/)
- For k8s visualization tools,  installing [kube-dash](https://www.digitalocean.com/community/conceptual-articles/kubernetes-visualization-tools#kubernetes-dashboard-kube-dashboard), we installed [headlamp](https://headlamp.dev/docs/latest/installation/) instead.  Very nice tool to visualize k8s.
- There is a Medium article on [Raspberry Pi Kubernetes: A Hassle-Guide with Ansible Magic](https://ebenamor.medium.com/raspberry-pi-kubernetes-a-hassle-guide-with-ansible-magic-5e70ec4d5ec9). ToDo
- Installed [Headlamp](https://headlamp.dev/)


## Step 5: GPU


## Step 6: Priority 
Partially worked, except there is no GPU so many pods cannot be deployed on the nodes.

- Here is an [example](https://medium.com/@muppedaanvesh/a-hands-on-guide-to-kubernetes-priority-classes-%EF%B8%8F-e4d37d789311) of priority class without GPU. ([PDF](./Kubernetes_Priority_Classes.pdf))
- [How to delete the applied pods](https://www.google.com/search?q=how+to+remove+running+pod+using+yaml&oq=how+to+remove+running+pod+using+yaml&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigATIHCAMQIRigATIHCAQQIRigATIHCAUQIRigATIHCAYQIRifBTIHCAcQIRifBTIHCAgQIRifBTIHCAkQIRiPAtIBCDg2ODlqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8)
- [SSH Jump Host](https://wiki.gentoo.org/wiki/SSH_jump_host) inside ```.ssh/config```
## Nest Steps: 

- YouTube video tutorial on [Prometheus, Grafana & Kubernetes: Installation + Monitoring](https://www.youtube.com/watch?v=r45DkTMMouc) by Rayan Slim.
    - Tested on k8s master node (VM), k0
    - Uses helm charts in [Prometheus Community Kubernetes Helm Charts](https://github.com/prometheus-community/helm-charts)
    - Used SSH tunnels to access localhost:port in the video. See [SSH tunnel error code](https://www.google.com/search?q=expose+port+but+see+channel+4%3A+open+failed%3A+connect+failed%3A+Connection+refused&oq=expose+port+but+see+channel+4%3A+open+failed%3A+connect+failed%3A+Connection+refused&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRiPAtIBCTIwNzU4ajBqN6gCALACAA&sourceid=chrome&ie=UTF-8), and [how to create SSH tunnels](https://www.google.com/search?q=how+to+create+ssh+tunnel+with+a+port+open&oq=how+to+create+ssh+tunnel+with+a+port+open&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigATIHCAMQIRigATIHCAQQIRigATIHCAUQIRirAjIHCAYQIRifBTIHCAcQIRiPAtIBCTEzNDU1ajBqN6gCALACAA&sourceid=chrome&ie=UTF-8)
    - Check if a port was exposed or not 

    - Uses YAML code in [application-monitoring-prometheus](https://github.com/rslim087a/application-monitoring-prometheus)
    - many other good materials on [Rayan Slim's page](https://rslim087a.github.io/rayanslim/)

## ToDo: Slurm Docker Cluster
- Here is the repo for the [Slurm Docker Cluster](https://github.com/stackhpc/slurm-k8s-cluster/blob/main/README.md)


## Trouble Shooting

### missing PKI content:

On [this post](https://github.com/kubernetes/kubernetes/issues/82178), a few lines can be used to recreate PKI certs:
```
kubeadm reset -f
kubeadm init phase certs all --control-plane-endpoint=drk8s.example.com:6443 --apiserver-cert-extra-sans=localhost --v=9
kubeadm init phase kubeconfig all --control-plane-endpoint=drk8s.example.com:644
kubeadm init --control-plane-endpoint drk8s.example.com:6443 --pod-network-cidr=10.244.0.0/16 --upload-certs --v=9 | tee kubeadm-output.txt
```

### Check kubelet failure reason
```
sudo journalctl -xeu kubelet
```

### Error on API Group list

- Error on ["couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s"]()

### Too Many Open Files

- Stackoverflow post on [listing open files](https://stackoverflow.com/questions/37067434/kubernetes-cant-start-due-to-too-many-open-files-in-system#:~:text=If%20you%20need%20to%20change,sudo%20systemctl%20restart%20docker.service)
- Article on how to fix [Too Many Open Files] (https://ploi.io/documentation/server/how-do-i-fix-the-too-many-open-files-error).
- 

### Migrate worker nodes into Cilium

- Tried the Step 6 on [this article](https://docs.cilium.io/en/stable/installation/k8s-install-migration/), to install cilium first, then add worker nodes.  But later rolled it out using kubectl delete...

