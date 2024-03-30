## Disclaimer.
The content on this account/repository provided solely for educational and informational purposes.
It is not intended for use in making any kind of business, investment and/or legal decisions.
Although every effort has been made to keep the information up-to-date and accurate, no representations and/or warranties, express and/or implied, completeness, accuracy, reliability, suitability, and/or availability of the content.

### K3S Single Node Deployment.
Setup single node [k3s](https://docs.k3s.io/) cluster.

### Installing k3s.
First find out latest stable release of k3s [here](https://github.com/k3s-io/k3s/releases/latest). Replace this with `LATEST_STABLE_VERSION` in below url. Once done then download the binary and install on the system.
```bash
# Download and install k3s binary.
wget https://github.com/k3s-io/k3s/releases/download/LATEST_STABLE_VERSION/k3s
mv k3s /usr/bin/k3s
chmod 755 /usr/bin/k3s

# Create symlinks.
ln -sf /usr/bin/k3s /usr/bin/kubectl
ln -sf /usr/bin/k3s /usr/bin/crictl
ln -sf /usr/bin/k3s /usr/bin/ctr
```

#### Installing systemd service for k3s.
The [Systemd Service File](./configs/k3s.service) provided here start `k3s` with default minimal configurations. This may not be correct configuration for all the environment. For detailed info check [k3s systemd service configuration](./configs/k3s-systemd-service-configuration.md).  
`k3s` by-default pull images from `docker.io/rancher/` registry. If the `docker.io` domain is not accessible then `k3s` will not start. For `air-gap` installation follow [here](https://docs.k3s.io/installation/airgap).
```bash
cp configs/k3s.service /etc/systemd/system/k3s.service
chmod 644 /etc/systemd/system/k3s.service
systemctl daemon-reload
systemctl enable --now k3s.service
```

#### Configure k3s config.
By default `k3s` stores config file at `/etc/rancher/k3s/k3s.yaml`. Following additional configuration requires for `kubectl` and `helm` tools to work.
```bash
mkdir -p ${HOME}/.kube
cp -a /etc/rancher/k3s/k3s.yaml ${HOME}/.kube/config
```

#### Accessing k3s Cluster from other systems.
It may requires to directly access the `k3s` cluster from some other systems in the network. In this case following additional configuration requires.
```bash
# Firewall allow tcp port 6443.
ufw allow 6443/tcp.
```

On other system, create a file `~/.kube/config`. In this file add the contents of the `/etc/rancher/k3s/k3s.yaml` file. In the `~/.kube/config` file replace the loopback ip address to the k3s system ip address.

### Helm.
For installing `helm` follow [here](./configs/installing-helm.md)

[Interacting with k3s cluster](./configs/interacting-with-k3s-cluster.md)
