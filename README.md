# my-k3s-setup

Simply create a Kubernetes (k3s) cluster with ssh accounts on the cluster nodes (debian based)

## Usage

Use the `./init` script to install a cluster node:
If your provider (like *netcup*) supports a final installation script, copy this script to the textbox, or use the script direct on the server.

The script installs needed components (git and curl) and clones this repo to the `/opt` directory on the server.

In a k3s installation you have a first server to install. The installation only needs the *clustername* to install this node - set a meaningful clustername to the last line of `./init` script.
A clustername could be `k3s-dev`, `my-k3s-cluster`, `testcluster` or what ever you want.

If this node is running connect to it with ssh - you can only use your username, root access is disabled for ssh in installation!
On the node execute `sudo print-k3s-config` - which will give you the IP of the first node and the token to connect new nodes to the cluster.

With this you can create more cluster nodes by modifying the last line of `./init` script:  
`./customize --silent <ip> <token>``

## Configuration

1. SSH Account(s) on cluster nodes  
   To create user accounts on the cluster nodes, create one directory for each user in `./users`. The name of the directory will be the username on cluster node.  
   Put a file `authorized_keys` with one ore more public keys of the user into the directory to give him access to the cluster nodes.  
   *Be aware*: Every user created by this mechanism has **sudo rights**!
2. Configure the installation of k3s.  
   In the file `./config/k3s-config.yml` you can set configuration options for installation of the cluster nodes:  
   https://docs.k3s.io/installation/configuration