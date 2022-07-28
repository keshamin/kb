---
title: "Yandex Cloud"
date: 2022-07-25T12:41:36+03:00
draft: false
---

# Yandex Cloud

## Resource Structure in Yandex Cloud

{{< figure src="./images/resource_structure.png" >}}

As a rule:
- 1 cloud == 1 company
- 1 catalog == 1 project

**Resource Manager** is responsible for organising resources in a structure and assigning permissions.

There are 2 types of roles:
- primitive predefined roles: global roles through all the services
  - viewer
  - editor
  - admin
- service roles: granular roles per each single service
fygbyvghcgh
Roles are inherited: 
- `editor` on a Cloud can manage resources in any catalog of the Cloud
- `editor` on a Catalog can manage only the resources withing that Catalog

## Users

There are 3 types of users:
- Yandex ID
- Federative account, provided by a supported external authentication system, e.g. Microsoft ActiveDirectory
- Service account

**Identity and Access Management** service is responsible for checking permissions when a user performs any action:
 {{< figure src="./images/authorization.png" >}}

## VPC

To group and isolate resources **Virtual Private Cloud** (VPC) is used. 

VPC can have unlimited number of **Subnets**. By default, for every VPC 3 subnets are created - for each **Availability Zone**. The subnets must not interfere in terms of IPv4 adresses. 
By default subnets do not have an access to the Internet. To enable it, you can:
- [enable "NAT to Internet" option](https://cloud.yandex.ru/docs/vpc/operations/enable-nat) (in Preview), 
- or [set up your own NAT instance on Compute VM](https://cloud.yandex.ru/docs/tutorials/routing/nat-instance#configure-static-route).  
If a Compute VM has a public IP and is accessible from the Internet, and can access the Internet itself as well. 

All resources within a VPC can access each other by internal addresses, no matter of which subnet they are assigned to. 

To manually manage routing within a subnet, **Routing Tables** are used.

**Security Groups** (in Preview) are defined in VPC and then can be assigned to network resources to controll firewall rules.

## Compute

Compute service creates **Virtual Machines** (VM). VMs are created from image: an operating system (Ubuntu, CentOS, Windows, ...) or a preconfigured software (Postgres, NAT Instance, VPN Server, ...).
**Preemtible** VMs can be turned off when the compute resources are requested by regular VMs. And then they restart when the resources are available again, without time guaranties. Good for testing, orchestrated batch jobs, or K8s cluster.

**Snapshot** is a state of a filesystem at some point in time. It is replicated in all AZs and can be used to restore a replica of some VM. 

**Image** is similar to snapshot, but is more performant in terms of restore time, thanks to the way of how snapshots and images are implemented under the hood.

**VM Groups** or Instance Groups are to create a set of VMs with similar configuration (resources, networking) by a template. They are capable of autoscaling basing on CPU load or other custom metric. 

### Access private VM via SSH

There are several ways to achieve that:
- First SSH to a public instance (e.g. NAT instance) in the same VPC and then SSH to the private one
- Setup a VPN server to access the whole private network space
- [Use a Serial Console](https://cloud.yandex.ru/docs/compute/operations/serial-console/connect-ssh); it is turned on/off in VM settings and should be turned off when not used. 

## Object Storage

### Access Control

The access to objects is controlled by 3 mechanisms:
- IAM roles
- Access Control List (ACL)
- Bucket Policy

Here's how the access is checked:
{{< figure src="./images/object_storage_access.webp" >}}

#### Which mechanism to choose?

- IAM roles are **always** checked, it covers basic use cases
- Bucket Policy allows to apply more complex criterias and conditions
- ACL allows to apply per-object rules

### Pre-signed URL

Pre-signed url is another option to provide access to object storage. 
- the link is time-limitted (seconds to days)
- it includes the action that is permitted and a signature for authentication
