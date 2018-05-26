# Ansible role: AWS VPC Route tables

This role handles the creation of Route tables for a VPC in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-route-table.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-route-table)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                      | Description                  |
|-------------------------------|------------------------------|
| `aws_vpc_route_table_profile` | Boto profile name to be used |


## Example definition

#### Required parameter only

```yml
aws_vpc_route_tables:
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    routes:
      # Example for Internet gateway
      - dest: 0.0.0.0/0
        type: igw
      # Example for NAT GW by name
      - dest: 185.28.100.13/32
        type: nat
        name: my-nat-gw-name
      # Example for NAT GW by filter
      - dest: 185.28.100.13/32
        type: nat
        filter:
          - key: "tag:Name"
            val: my-nat-gw-name
          - key: "tag:env"
            val: production
      # Example for Instance by name
      - dest: 185.28.100.13/32
        type: instance
        name: my-instance-name
      # Example for Instance by filter
      - dest: 185.28.100.13/32
        type: instance
        filter:
          - key: "tag:Name"
            val: my-instance-name
          - key: "tag:env"
            val: production
      # Example for Interface by name
      - dest: 185.28.100.13/32
        type: interface
        name: my-interface-name
      # Example for Interface by filter
      - dest: 185.28.100.13/32
        type: interface
        filter:
          - key: "tag:Name"
            val: my-interface-name
          - key: "tag:env"
            val: production
      # Example for VPC Peering by name
      - dest: 185.28.100.13/32
        type: peering
        name: my-peering-name
      # Example for VPC Peering by filter
      - dest: 185.28.100.13/32
        type: peering
        filter:
          - key: "tag:Name"
            val: my-peering-name
          - key: "tag:env"
            val: production
    subnets:
      # Example for subnet by name
      - name: my-subnet-name
      # Example for subnet by cidr
      - cidr: 172.25.2.0/24
      # Example for subnet by id
      - id: subnet-0fead839
      # Example for subnet by filter
      - filter:
          - key: "tag:Name"
            val: my-subnet-name
          - key: "tag:env"
            val: production
```

#### All available parameter
```yml
aws_vpc_route_tables:
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    region: eu-central-1
    tags:
      - key: Name
        val: devops-test-route-table
      - key: env
        val: production
      - key: department
        val: devops
    routes:
      # Example for Internet gateway
      - dest: 0.0.0.0/0
        type: igw
      # Example for NAT GW by name
      - dest: 185.28.100.13/32
        type: nat
        name: my-nat-gw-name
      # Example for NAT GW by filter
      - dest: 185.28.100.13/32
        type: nat
        filter:
          - key: "tag:Name"
            val: my-nat-gw-name
          - key: "tag:env"
            val: production
      # Example for Instance by name
      - dest: 185.28.100.13/32
        type: instance
        name: my-instance-name
      # Example for Instance by filter
      - dest: 185.28.100.13/32
        type: instance
        filter:
          - key: "tag:Name"
            val: my-instance-name
          - key: "tag:env"
            val: production
      # Example for Interface by name
      - dest: 185.28.100.13/32
        type: interface
        name: my-interface-name
      # Example for Interface by filter
      - dest: 185.28.100.13/32
        type: interface
        filter:
          - key: "tag:Name"
            val: my-interface-name
          - key: "tag:env"
            val: production
      # Example for VPC Peering by name
      - dest: 185.28.100.13/32
        type: peering
        name: my-peering-name
      # Example for VPC Peering by filter
      - dest: 185.28.100.13/32
        type: peering
        filter:
          - key: "tag:Name"
            val: my-peering-name
          - key: "tag:env"
            val: production
    subnets:
      # Example for subnet by name
      - name: my-subnet-name
      # Example for subnet by cidr
      - cidr: 172.25.2.0/24
      # Example for subnet by id
      - id: subnet-0fead839
      # Example for subnet by filter
      - filter:
          - key: "tag:Name"
            val: my-subnet-name
          - key: "tag:env"
            val: production
```