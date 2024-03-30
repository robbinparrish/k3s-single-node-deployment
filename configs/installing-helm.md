## Installing helm.
The [helm](https://helm.sh/docs/) utility will be required to install the `helm-chart` in the `k3s cluster`.  
First find out latest stable release of helm [here](https://github.com/helm/helm/releases/latest). Replace this with `LATEST_STABLE_VERSION` in below url. Once done then download the binary and install on the system.
```bash
wget https://get.helm.sh/helm-LATEST_STABLE_VERSION-linux-amd64.tar.gz -O /tmp/helm.tar.gz
tar -xvf /tmp/helm.tar.gz -C /tmp/
mv /tmp/linux-amd64/helm /usr/bin/helm
chmod +x /usr/bin/helm
rm -rf /tmp/linux-amd64/ /tmp/helm.tar.gz
```
