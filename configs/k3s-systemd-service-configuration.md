## K3S Systemd Service Configuration.
The systemd service configuration file contains some additional configuration like mentioned below.  
Various configuration options for `k3s server` can be found [here](https://docs.k3s.io/cli/server).

- Add-ons configuration.

    Some default additional add-ons like `traefik` and `metrics-server` are currently disabled. If requires then remove following from the systemd file.
    ```
    --disable=traefik --disable=metrics-server
    ```

- CIDR Network range.

    `k3s` uses default CIDR network range for internal communication. If changes requires then update different CIDR range in the systemd file.
    ```
    --cluster-cidr="10.42.0.0/16" --service-cidr="10.43.0.0/16"
    ```

- NodePort range.

    `k3s` uses a port range from systems dynamic port range. If need to modify this to contain only small number of ports or some other range then update different ports range in the systemd file.
    ```
    --service-node-port-range="30000-32767"
    ```

- Data storage.

    `k3s` uses default data directory from root (/) partition. On some cases it may need to change this to some other path or additional mounted drive instead of OS drive. If changes requires then update different directory in the systemd file.
    ```
    --data-dir="/var/lib/rancher"
    ```

    If this directory is changed to some other path then will need to create a symlink since `k3s` default uses some configuration files from default data directory.
    ```bash
    ln -sf PATH_TO_STORAGE_DIR_FOR_K3S /var/lib/rancher
    ```

- Configuration for kubelet.

    A detailed configuration can be found [here](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/).

    - Log configuration for pods. If changes requires then update different directory in the systemd file.
    ```
    --kubelet-arg "--container-log-max-files=2"
    --kubelet-arg "--container-log-max-size=10Mi"
    ```

    - Image garbage collection configuration. If changes requires then update different directory in the systemd file.
    ```
    --kubelet-arg "--image-gc-high-threshold=60"
    --kubelet-arg "--image-gc-low-threshold=50"
    ```
