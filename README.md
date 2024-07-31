# Chart
A sample chart to deploy an application. It's using Wordpress as a
placeholder, and is missing a required MySQL compatible database, to
add it to the NetworkPolicy to allow them to connect, the values
to specify database information like hostname, replicas, external or
helm-managed, another config-map for any database configuration, and a
stateful set to actually run the database if it's helm-managed.

# Kubernetes environment
An internet gateway with NAT connects to following private networks:
- kube-api
- worker

There is one public network `service` for services to be exposed on. 

They have egress to internet but no ingress except to one public
network that only contains a virtual machine to be used as a jump box.

The jump box has a port exposed for SSH, this is to limit the clusters
exposure to unauthorized use. 

The kube-api and worker networks can connect through the kubernetes
API port, important for the scheduler to schedule and for any cluster
service accounts to access kubernetes resources.

The kube-api nodes will need their host's cloud container storage
interface to provision volumes or else we'll need an extra private
network for storage that can communicate with worker and kube-api
networks. In that case, nodes on this network will have a special
annotation, and large storage pools to run OpenEBS as a container
storage interface. Either way we will need to backup the volumes, for
this I will install Velero and backup to an S3-compatible object
store.

Like wise, using the host's cloud controller managers service
controller to expose services with a load balancer. 

The virtual machines will have Ubuntu 24.04 and all but the jump box
will also have k0s version 1.30.3+k0s installed using a configuration
management tool to install then register nodes with each other and add
ny necessary annotations or labels.
