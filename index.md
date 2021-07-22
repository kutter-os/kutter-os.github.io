# Kutter

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

----

The download is around 320 MB, with all batteries included.

Kubernetes (`kubeadm`) requires 2 vCPU and 2 GB memory.

It is available for `amd64` (VM) and `arm64` (Raspberry Pi)

There is currently no public release of Kutter OS available.

----

Written by Anders F Björklund <https://github.com/afbjorklund>

Kutter OS logo credit: [By KDS444 - Own work, CC BY-SA 3.0](https://commons.wikimedia.org/w/index.php?curid=33382230)
