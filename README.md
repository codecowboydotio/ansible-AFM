# F5 AFM ansible playbooks

This repository contains samples to do various things with AFM on an F5 bigip.


## update_afm_from_ec2.yml

This playbook is an example of updating AFM rules with subnets from AWS. 
The subnets are searched for by tag name and value.

Essentially, if you tag a subnet, and run the playbook, and AFM rule will be created.

### Pre-requisites
You need a bigip :)

1. BigIP with AFM modules installed.
2. Host that has ansible installed
3. f5-sdk python module installed
4. AWS IAM access key and secret key

### Playbook variables

There are a number of variables in the playbook, these can be set statically or can be passed using the "--extra-vars" option from the command line.

```
    my_subnets: [] - A dictionary that is used to build up an addresslist. No need to change this.

    bigip_server:  - The IP address of the BIGIP that you would like to configure.

    bigip_user:    - BIGIP username - user must have permissions to configure BIGIP.

    bigip_password:  - BIGIP user password.

    bigip_validate_certs: - If you are using self signed certificates, set to no, otherwise can be set to yes.

    bigip_policy_name: - Name of the policy to create. This can be anything. f

    bigip_rule_name: Name of the rule to create. 

    bigip_fw_rule_dest_addr: Destination address

    bigip_address_list_name: Name of the addresslist object to create. 

    tag_filter: The tag that the subnets have.b

    region: AWS region name that you want to run against. The most up to date list is here (https://docs.aws.amazon.com/general/latest/gr/rande.html)

    playbook_debug: This turns on additional debugging (set to true if you would like additional debugging).
```

### General Notes

As the F5 modules can be delegated to localhost, there is no need to have an ssh key on each F5 device. This is desirable in heavily outsourced environments, or 
environments where the separation of duties requires it.

This means that the Ansible control node needs to have a local ssh key installed, as the task is delegated to localhost.

### Running

```
ansible-playbook update_afm_from_ec2.yml
```



