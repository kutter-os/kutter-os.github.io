# Kutter - "välseglande enmastad skuta"

The aim is to make a minimal OS for running Kubernetes.

Kutter is the swedish name for the sailing vessel [Cutter](https://en.wikipedia.org/wiki/Cutter_(boat)).

<img alt="origami boats sailing sea" src="/assets/origami.jpg" />

<a href="http://www.freepik.com">Designed by brgfx / Freepik</a>

----

Starting up a Kubernetes node requires a couple of things:

* An operating system (OS), running the Linux kernel.

* A Container Runtime Interface (CRI), such as Docker.

* A Container Network Interface (CNI), such as Flannel.

* The programs and images, for running Kubernetes.

With the requirements in place, a new node is started like:

* Control Plane

  `kubeadm init [flags]`

* Worker node

  `kubeadm join [api-server-endpoint] [flags]`

See ["Creating a cluster with kubeadm"](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) for all the details.

```console
# kubeadm init --pod-network-cidr=10.244.0.0/16
...
# export KUBECONFIG=/etc/kubernetes/admin.conf
# kubectl apply -f /etc/kubernetes/flannel.yml
```

----

pods
```
NAMESPACE     NAME                                READY   STATUS
kube-system   coredns-558bd4d5db-ngwz5            1/1     Running
kube-system   coredns-558bd4d5db-s9v8w            1/1     Running
kube-system   etcd-buildroot                      1/1     Running
kube-system   kube-apiserver-buildroot            1/1     Running
kube-system   kube-controller-manager-buildroot   1/1     Running
kube-system   kube-flannel-ds-vvf28               1/1     Running
kube-system   kube-proxy-4sfql                    1/1     Running
kube-system   kube-scheduler-buildroot            1/1     Running
```

pstree
```
systemd─┬─acpid
        ├─7*[containerd-shim─┬─pause]
        │                    └─10*[{containerd-shim}]]
        ├─containerd-shim─┬─etcd───10*[{etcd}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─kube-apiserver───7*[{kube-apiserver}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─kube-controller───4*[{kube-controller}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─kube-scheduler───6*[{kube-scheduler}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─kube-proxy───5*[{kube-proxy}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─flanneld───7*[{flanneld}]
        │                 └─10*[{containerd-shim}]
        ├─containerd-shim─┬─pause
        │                 └─11*[{containerd-shim}]
        ├─2*[containerd-shim─┬─coredns───6*[{coredns}]]
        │                    └─10*[{containerd-shim}]]
        ├─dbus-daemon
        ├─dockerd─┬─containerd───8*[{containerd}]
        │         └─15*[{dockerd}]
        ├─haveged
        ├─kubelet───13*[{kubelet}]
        ├─sh───pstree
        ├─sshd
        ├─systemd-journal
        ├─systemd-network
        ├─systemd-resolve
        ├─systemd-timesyn───{systemd-timesyn}
        └─systemd-udevd
```

----

Building all the required software is done using [Buildroot](https://buildroot.org/).

The download is around 300 MB, with all batteries included:

- **buildroot**, the OS boot with pre-installed software (140M)

- **images**, the compressed tarballs of docker images (160M)

See <https://github.com/afbjorklund/buildroot4kubernetes>

----

Kubernetes (`kubeadm`) requires 2 vCPU and 2 GB memory.

Some 20 GB of free disk space is required for the runtime.

It is available for `amd64` (VM) and `arm64` (Raspberry Pi)

There is currently no public release of Kutter OS available.

Written by Anders F Björklund <https://github.com/afbjorklund>

----

Kutter OS logo credit: [By KDS444 - Own work, CC BY-SA 3.0](https://commons.wikimedia.org/w/index.php?curid=33382230)
