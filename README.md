# Deploy a Managed K8s Cluster

I'll use Vagrant and VirtualBox to create a 3 VMs with Red Hat Enterprise Linux (RHEL) OS.

The VMs spcifications are as follows:

- Memory: 4096 MB
- CPUs: 2 cores

the Control Plane Node
cp-001, 192.168.101.100

the Worker Nodes:
node-001, 192.168.101.101
node-002, 192.168.101.102

> Note: you can change the VMs specifications in the Vagrantfile.

## Pre-requisites

- Developer account on [Red Hat Developer](https://developers.redhat.com/)
- [Vagrant](https://www.vagrantup.com/downloads.html)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Visual Studio Code](https://code.visualstudio.com/download)

## On the Host Machine (Development PC)

Execute the following commands:

```sh
vagrant plugin install vagrant-hostmanager
```

```sh
vagrant up
```

ssh to the VMs using vagrant ssh:

```sh
vagrant ssh <vm-name>
```

or

```sh
ssh vagrant@<vm-ip>
```

Inside each VM, execute the following commands:

```sh
sudo subscription-manager register --username='<your-username>' --password='<your-password>' --force
sudo yum update -y
```

> Note: the username and the password for the Red Hat Developer account.

### To be continued

### to-do

I will add more than way to setup k8s cluster

- [ ] Add a Diagram
- [ ] Add References
- [ ] Setup VSCode
    - [ ] Workspace
    - [ ] devcontainer
- [ ] Configuration Options:
    - [ ] Ansible
    - [ ] Makefile
    - [ ] Vagrantfile
- K8s dev tools:
    - [ ] Helm
    - [ ] Docker
    - [ ] Kubectl
    - [ ] Lens
- [ ] Setup Pipeline With:
    - [ ] GitLab CI/CD
    - [ ] GitHub Actions
- [ ] Setup Monitoring:
    - [ ] Prometheus
    - [ ] Grafana
- [ ] Setup Logging:
    - [ ] ELK Stack
- [ ] Setup Notification:
    - [ ] Slack
    - [ ] MS Teams
    - [ ] Email
- [ ] Apply GitOps Practices with ArgoCD
