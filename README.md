# Kutter

The aim is to make a minimal OS for running Kubernetes.

Kutter is the swedish name for the sailing vessel [Cutter](https://en.wikipedia.org/wiki/Cutter_(boat)).

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

Logo credit: [By KDS444 - Own work, CC BY-SA 3.0](https://commons.wikimedia.org/w/index.php?curid=33382230)
