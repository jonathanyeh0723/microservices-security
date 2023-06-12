# microservices-security
To adopt a hardened Flask application, Docker, and Kubernetes environment.

## Architecture
![img_1_architecture](./resources/security_architecture_design.png)

## Runtime Monitoring

### Falco

```
vagrant up
vagrant ssh
```

```
sudo ssh-copy-id -p 2222 -i ~/.ssh/id_rsa root@localhost
```

```
rke up
```

```
kubectl --kubeconfig kube_config_cluster.yml get pods -A
kubectl --kubeconfig kube_config_cluster.yml get node
```


```
rpm --import https://falco.org/repo/falcosecurity-packages.asc
curl -s -o /etc/zypp/repos.d/falcosecurity.repo https://falco.org/repo/falcosecurity-rpm.repo
zypper -n update

zypper -n install dkms make
# If the package was not found by the below command, you might need to run `zypper -n dist-upgrade` in order to fix it. Rebooting the system may be required.
zypper -n install kernel-default-devel-$(uname -r | sed s/\-default//g)
# If you use the falco-driver-loader to build the BPF probe locally you need also clang toolchain
zypper -n install clang llvm
# You can install also the dialog package if you want it
zypper -n install dialog

zypper -n install falco

