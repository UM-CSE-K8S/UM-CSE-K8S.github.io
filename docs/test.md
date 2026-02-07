# Actual Progress

We have tested following:

## Tested Steps

- On vyl-hpe.eecs.umich.edu
- create three Ubuntu 24.04 LTS VMs: ```k0, k1, k2```
- We are not exactly following the [exact commands in index.html](https://um-cse-k8s.github.io/index.html) but the most of the steps are similar.  So see details below.

## Step 1-4
- Medium article on [How to Install Kubernetes Cluster on Ubuntu 24.04 LTS (Step-by-Step Guide)] and its [PDF](./How_to_Install_K8s.pdf).
- When CNI does not work, debug it with [these hints](https://www.google.com/search?q=after+install+kubernetes+on+master+node%2C+the+node+is+NotReady&oq=after+install+kubernetes+on+master+node%2C+the+node+is+NotReady&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRiPAtIBCTExMjAyajBqN6gCALACAA&sourceid=chrome&ie=UTF-8)
- For missing CNI, if Calico, use a command in the comment by Michael as ```kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml```
- For missing CNI, use cilium with [how to install cilium CNI for kubernetes](https://www.google.com/search?q=CANNOT+REACH+PORT+9090+AFTER+INSTALL+PEOMETHEUS&oq=CANNOT+REACH+PORT+9090+AFTER+INSTALL+PEOMETHEUS+&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIJCAEQIRgKGKABMgkIAhAhGAoYoAEyCQgDECEYChigATIJCAQQIRgKGKABMgkIBRAhGAoYoAEyCQgGECEYChirAjIJCAcQIRgKGKsCMgcICBAhGJ8FMgcICRAhGJ8F0gEJMTIyNjdqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8)
- There is a Medium article on [Raspberry Pi Kubernetes: A Hassle-Guide with Ansible Magic](https://ebenamor.medium.com/raspberry-pi-kubernetes-a-hassle-guide-with-ansible-magic-5e70ec4d5ec9). ToDo
- Installed [Headlamp](https://headlamp.dev/)

## Step 5: GPU


## Step 6: Priority 
Partially worked, except there is no GPU so many pods cannot be deployed on the nodes.

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