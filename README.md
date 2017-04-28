# Heartbeat Cluster - Resource Agent - EC2PrivateIP

NO WARRANTY - Use at your own risk!

## Introduction
This is how we manage our heartbeat clusters in EC2. This was based loosely on several scripts available on google. This has only ever been tested on CentOS 6.8+. 

## What does this script do?
This acts as a resource agent for a hearbeat (haresources) cluster. It will "assign" an additional private IP address to the primary network interface (ENI) of an EC2 Instance. It has the ability to "unassign" during a "stop" operation, butthat is disabled because that causes the Elastic IP to become disassociated from the private IP.

## Requirements

   * bash (well its written in bash)
   * jq: `yum install jq` (EPEL)
   * awscli: http://docs.aws.amazon.com/cli/latest/userguide/awscli-install-bundle.html
      * NOTE: I used /opt/awscli


## Usage

   * Place EC2PrivateIP script into `/etc/ha.d/resource.d`
   * EDIT EC2PrivateIP script to define the region (if you are not in us-east-1)
   * Add `EC2PrivateIP::10.1.2.10` to /etc/ha.d/haresources
   * Add `IPAddr::10.1.2.10/24` as well to /etc/ha.d/haresources


NOTE: This script also has a setting for proxy, as long as your hostname doesn't include proxy. It sources `/usr/local/etc/proxy.sh` to get the proxy servers.

NOTE2: This is about the 4th version of this script, and it may have some old cruft laying about in it (sorry). It does have the capability of managing a "Public" IP address, so long as you associate the Elastic IP to a secondary IP address. See https://aws.amazon.com/articles/2127188135977316 for details. This is very messy, but functional (works for me). It has lots of room for improvement!

Let me know if this is useful, and PRs are appreciated.

~tommy
