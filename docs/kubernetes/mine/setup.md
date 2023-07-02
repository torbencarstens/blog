# Setup

## terraform

[terraform](https://github.com/torbencarstens/rke2-build-hetzner) sets up the servers (master/agent), loadbalancer and private network. 

## ansible

[ansible-base](https://github.com/torbencarstens/ansible-base) contains playbooks, role references, vaults, environments specific variables and is the repo in which `ansible-playbook` is executed.

[ansible-role-os-baseconfig](https://github.com/torbencarstens/ansible-role-os-baseconfig) sets up the underlying os (`debian-11` as of writing (02.07.2023)).

We'll only be using images which are offered by hetzner as part of their [`Standard images`](https://docs.hetzner.com/robot/dedicated-server/operating-systems/standard-images).

[ansible-role-os-rke2](https://github.com/torbencarstens/ansible-role-rke2) sets up the rke2 cluster itself. This includes:

- downloading the newest tarball
- writing the server/agent config
- configuring cilium/[...] (via `HelmChartConfig`)
- firewall config
- rke2-{agent,server} start/enable
- etcd configuration

[ansible-role-os-cluster-baseconfig](https://github.com/torbencarstens/ansible-role-cluster-baseconfig)

## argocd

> In contrast to ansible I won't document each downstream argocd app here since they will change more often
> 
> ansible roles will be fairly static since they're just setting up the initial cluster

[argocd-bootstrap](https://github.com/OpenAlcoholics/argocd-bootstrap) is installed by [ansible-role-os-cluster-baseconfig](https://github.com/torbencarstens/ansible-role-cluster-baseconfig).

argocd later takes over this application in the [argocd-bootstrap](https://github.com/OpenAlcoholics/argocd-bootstrap) app itself.
