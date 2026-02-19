# Kubernetes Mockup System



We have installed following VMs to test Kubernetes on ```gaia.eecs.umich.edu```:

| hostname | Role   | IP Address    | Hardware | Software |
|----------|--------|---------------|----------|---------|
| k0       | master | 192.168.8.146 | 2 core 8G Mem 50GB HDD | Ubuntu 24.04.3 LTS |
| k1       | worker | 192.168.8.147 | 2 core 8G Mem 20GB HDD | Ubuntu 24.04.3 LTS |
| k2       | worker | 192.168.8.148 |  2 core 8G Mem 20GB HDD | Ubuntu 24.04.3 LTS |
| k2       | worker | 192.168.8.149 |  2 core 8G Mem 20GB HDD | Ubuntu 24.04.3 LTS |

## How to Access

Users should prepare following steps to access the cluster:

- Be able to access ```gaia.eecs.umich.edu```
  - Request access via [CSE DCO](https://www.eecs.umich.edu/dco/about.php), or from server admin staff.
  - On UM Campus or have [UM Net VPN](https://its.umich.edu/enterprise/wifi-networks/vpn/getting-started) while off campus. 
  - SSH via their UM uniqname and Password initially as ```ssh uniqname@gaia.eecs.umich.edu```
  - Optional: setup public key authentication with these [steps](https://www.redhat.com/en/blog/configure-ssh-keygen) OR [here](https://www.hpc.temple.edu/mhpc/hpc-technology/exercise4/ssh.html).
  - Optional: It is important to setup [SSH Jump Host](https://wiki.gentoo.org/wiki/SSH_jump_host) inside ```~/.ssh/config``` to easier access of VMs inside a physical server.  For example, we have the following setup to access ```k0``` using ```ssh k0``` via the jumphost ```gaia```. (Remember this requires one to setup the public key authentication from ```gaia``` to ```k0``` too!)
```
Host gaia
  HostName gaia.eecs.umich.edu
  User vyl
  IdentityFile ~/.ssh/id_rsa
Host k0
  HostName k0
  ProxyJump  gaia
```

## Create SSH Tunnels to Access Headlamp and Grafana

We have installed [Headlamp](https://headlamp.dev/) and [kube-prometheus-stack](https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack) on Kubernetes to visualize and monitor the k8s cluster respectively.  To access these two services on ```k0```, we need to create two tunnels to access their corresponding web fronts. 

### Access Headlamp via http://localhost:8080

- On your local laptop, assuming a MacBook, creating a tunnel from ```localhost:8080``` to ```localhost:8080``` as below:

vyl@UM-VYL-MBA-20 ~ %
``` bash
ssh -L localhost:8080:127.0.0.1:8080 k0
```
- Once the above command bring you onto ```k0```, obtain the token to be used to authenticate. Copy that token into your clipboard.

``` bash
kubectl create token headlamp-admin -n kube-system
```

- Then continue execute following command to forward the port of headlamp's 80 to localhost:8080. 
``` bash
kubectl port-forward svc/headlamp -n kube-system 8080:80
```

- Open a web browser on your laptop, and visit ```http://127.0.0.1:8080/```.  This should forward you to 
```http://127.0.0.1:8080/c/main/token```
and ask for a token.  
    - Paste what is stored in your clipboard in above step here and click "Authenticate". 
    - ![Screenshot](./headlamp-token.png)
- Once completed above steps, you should be able to see Headlamp UI to visualize various namespaces, pods, nodes, etc. instead this k8s cluster. 
    - ![Headlamp Map](./headlamp-map.png)

### Access Grafana via http://localhost:3000

Similar to the Headlamp steps, Grafana is available on port 3000, as steps below:

- On your local laptop, assuming a MacBook, creating a tunnel from ```localhost:3000``` to ```localhost:3000``` as below:

vyl@UM-VYL-MBA-20 ~ %
``` bash
ssh -L localhost:3000:127.0.0.1:3000 k0
```
- Once the above command bring you onto ```k0```, obtain the token to be used to authenticate. Copy that token into your clipboard.

``` bash
kubectl create token headlamp-admin -n kube-system
```

- Then continue execute following command to forward the port of Grafana's 80 to localhost:3000. 
``` bash
kubectl port-forward svc/prometheus-grafana -n monitoring 3000:80 &
```

- Open a web browser on your laptop, and visit ```http://127.0.0.1:3000/```.  This should forward you to  ```http://127.0.0.1:3000/login```
and ask for username and password.  
The default should be ```admin``` and ```prom-operator```.  Alternatively one can run this command to find out on the master node ```k0```:

```
kubectl get secret --namespace monitoring prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

- Once completed above steps, you should be able to see Grafana UI to visualize various parameters that Prometheus collected from this k8s cluster.  Prometheus UI will be discussed in a different WebUI (TBD) later.
    - For example, the [Grafana CPU Usage](http://localhost:3000/d/200ac8fdbfbb74b39aff88118e4d1c2c/kubernetes-compute-resources-node-pods?orgId=1&refresh=10s) should show CPU utilization for various PODS below [CPU Usage](./grafana-cpu.png)

## How to set up
To see the detailed steps to setup this VM based cluster, see [install.html](./install.html) (Working in progress).