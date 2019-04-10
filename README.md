# Ansible - AWS CloudFormation

This repo contains Ansible code and AWS CloudFormation templates for the
provisioning of AWS resources.

#Steps to work on (see Jenkins file)

 
## Requirements

* Install [Ansible](http://docs.ansible.com/ansible/intro_installation.html).
* Set-up Ansible for [authenticating with AWS](http://docs.ansible.com/ansible/guide_aws.html#authentication).



### Register domain name

* Register a domain name using [AWS Route 53](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar.html).
* Create a [public hosted zone](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/AboutHZWorkingWith.html)
for the domain.
* Uncomment _hosted_zone_public_name_ in [group_vars/site/main.yml](../master/group_vars/site/main.yml) 
and insert the public hosted zone domain name.

### HTTPS

* [Create a certificate](https://aws.amazon.com/certificate-manager/) for *._hosted_zone_public_name_
  (i.e., name inserted for _hosted_zone_public_name_ in the previous step).
* Uncomment _ssl_certificate_id_ in [group_vars/site/main.yml](../master/group_vars/site/main.yml) 
  and insert the certificate ARN.

### Key name

* Uncomment _key_name_ in [group_vars/site/main.yml](../master/group_vars/site/main.yml) 
  and insert the name of the EC2 key pair that you want to use to connect to the EC2 instances.

## Provision network and site

    git clone git@github.com:bendbennett/ansible-aws.git
    cd ansible-aws/cloud-formation
    ansible-playbook basic-network.yml
    ansible-playbook site.yml 

## Remove network and site

    cd ansible-aws/cloud-formation
    ansible-playbook site-down.yml
    ansible-playbook basic-network-down.yml
     
## Network  

 First to deploy network use vpc.yml.
