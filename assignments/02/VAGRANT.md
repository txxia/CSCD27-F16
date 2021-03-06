# CSCD27: Vagrant Setup Guideline

## The virtual network

In the networking labs and assignment, we are going to setup a **virtual** penetration testing environment. This setup will allow us to attack and defend these virtual machines without interfering with each other (as we would if we were all tampering with a shared server). Despite being virtual, this setup is technically similar to a real one, at least for the attack and defense techniques that we are going to consider.

In this virtual penetration testing environment, we (as Mallory) want to eavesdrop and hijack the communication between Alice and Bob. Our virtual network has three virtual machines (abbreviated VM):

1. `Mallory` (ip=10.0.1.102) is the VM that we will use to run our attacks
2. `Alice` (ip=10.0.1.101) is the innocent victim that we want to attack
3. `Gateway` (ip=10.0.1.100) is the VM that gives Alice access to the internet. You can imagine that this machine is your internet box at home.

Bob is not part of our virtual network as this role will be played by the real [Mathlab](http://mathlab.utsc.utoronto.ca) server.

## Using Vagrant in the Linux Lab

To setup and interact with our virtual environment, we are going to use [vagrant](https://www.vagrantup.com/). The [vagrant configuration](https://raw.githubusercontent.com/ThierrySans/CSCD27-F16/master/assignments/02/code/Vagrantfile) provided for the assignment and the labs has been tailored to run on the linux lab.

Therefore, it is *strongly recommended* to do all the work in the lab as it will be hard to reproduce the same setup on your machine.

## Init (once and only once)

By default in the linux lab, vagrant stores the virtual machines in your home directory. Since you do not have enough space there, we are going to store the VMs in the `cscd27f16_space` directory. The following command configures vagrant's home directory:

```shell
$ echo "export VAGRANT_HOME=~/cscd27f16_space/.vagrant.d" >> ~/.profile
$ source ~/.profile
$ vboxmanage setproperty machinefolder ~/cscd27f16_space/.VirtualBox
```

Inside `cscd27f16_space`, clone the Github course repository:

```shell
$ cd cscd27f16_space
$ git clone https://github.com/ThierrySans/CSCD27-F16
```

The VMs are defined in the file `Vagrantfile` provided for assignment 02. Start all VMs for the first time:

```shell
$ cd ~/cscd27f16_space/CSCD27-F16/assignments/02/code
$ vagrant up
```

## Using the VMs

Assuming that you have cloned the Github repository for D27 and that you are in `SCD27-F16/assignments/02/code`

- Starting all VMs

```shell
$ vagrant up
```

- SSHing into VMs

```shell
$ vagrant ssh mallory
```

Once connected to Mallory, you should see the following prompt: `vagrant@mallory:~$`. You can do the same for `alice` and the `gateway`.

While working on the assignment or the labs, you will be asked to performed actions *as Mallory* or *as Alice* by using the proper VMs. Therefore, it is *strongly recommended* to have 3 terminal windows (or tabs) open:

 - one for the host (your actual ubuntu lab machine)
 - one for Alice
 - and two for Mallory

- Stopping all VMs (strongly recommended once you are done working)

```shell
$ vagrant halt
```

-Stop and restart all VMs

```shell
$ vagrant reload
```

## Verify the internet connectivity

Before starting working, verify that the machines are connected to the internet.

As either Mallory, Alice or the Gateway:

```shell
$ ping mathlab.utsc.utoronto.ca
```

If either Mallory or the Gateway do not have internet connection, ask immediately the instructor.

If Alice does not have the internet you try this fix:

*As Alice*:
```shell
vagrant@alice:~$ ping 10.0.1.100
```

*As Gateway*:
```shell
vagrant@gateway:~$ sh /vagrant/gateway/setup.sh
```

## Reset all VMs, Reset Vagrant and Reset VirtualBox

If something goes wrong with vagrant you can either reset all VMs and/or re-initialized vagrant.

1. reset the VMs

```shell
$ vagrant destroy
```

if the command above fails, you can destroy it manually:

```shell
$ rm -Rf .vagrant
```

2. re-initialize vagrant all together

```shell
$ rm -Rf ~/cscd27f16_space/.vagrant.d
```

3. re-initialize VirtualBox all together

```shell
$ rm -Rf ~/cscd27f16_space/.VirtualBox
```