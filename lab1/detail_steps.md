# Introduction

This lab involves an obfuscated script that uses `ip netns` and various other Linux networking tools to set up network namespaces and arrange them into a specific topology. The objective of this lab is to investigate the network topology after the script has been run. Your tasks include identifying the created namespaces, discovering how they are connected, determining the IP addresses assigned to each, and figuring out which namespaces can communicate with each other.

# Setup

### 1. Bring Up the `node1` VM

First, use the provided Vagrant file to bring up the `node1` virtual machine (VM).

```bash
vagrant up node1
```

### 2. SSH into `node1`

Once the VM is running, SSH into `node1` using the following command:

```bash
vagrant ssh node1
```

### 3. Navigate to the Lab Directory

After SSHing into the `node1` VM, navigate to the directory where the lab files are located:

```bash
cd /vagrant/lab1
```

This step is crucial to ensure you're in the correct directory to execute the scripts.

### 4. Run the Setup Script

Before running the setup script, it is recommended that you clear any existing `iptables` rules to avoid conflicts. This is suggested since the script is meant to run in a controlled lab environment.

```bash
../clear-fw.sh
```

Next, execute the obfuscated script to set up the network namespaces and topology:

```bash
./ob-create-lab1-mod4.sh
```

# Useful Tools

Here is a list of useful commands that can be used to investigate the network topology (some of these commands can be used inside or outside of a namespace):

- `ip netns list` - Lists all the network namespaces.
- `ip netns exec <namespace> <command>` - Executes a command inside the specified network namespace.
- `ip route` - Displays the routing table within a namespace.
- `ethtool` - Provides information about network interfaces.
- `ip link` - Shows the network interfaces and their status.
- `ping` - Tests the connectivity between IP addresses.
- `tshark` or `tcpdump` - Captures and analyzes network traffic.

Your goal is to draw the network topology by determining which namespaces exist, which veth pairs are present in each namespace, how these veths are connected, and what IP addresses are associated with each veth. Then, by examining the routing table and using connectivity tests, determine the reachability of the IP addresses within the topology.

# Clean Up

To revert any changes made during the lab (such as deleting namespaces), run the cleanup script:

```bash
./ob-del-lab1-mod4.sh
```

This will remove the namespaces and undo the network configuration set up by the script.
