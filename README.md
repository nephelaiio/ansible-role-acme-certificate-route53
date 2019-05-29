# nephelaiio.acme-dnschallenge-route53

[![Build Status](https://travis-ci.org/nephelaiio/ansible-role-acme-dnschallenge-route53.svg?branch=master)](https://travis-ci.org/nephelaiio/ansible-role-acme-dnschallenge-route53)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-nephelaiio.acme-dnschallenge-route53-blue.svg)](https://galaxy.ansible.com/nephelaiio/acme-dnschallenge-route53/)

An [ansible role](https://galaxy.ansible.com/nephelaiio/acme-dnschallenge-route53) to issue acme certificates with dns challenge verification using route53 name service

## Role Variables

The most common user overridable parameters for the role are

| required | variable | description | default |
| --- | --- | --- | --- |
| *yes* | acme_certificate_domain | the fqdn to generate an acme certificate for | ansible_fqdn |
| *yes* | acme_certificate_aws_accesskey_id | an ec2 key id with route53 management rights | lookup('env', 'AWS_ACCESS_KEY_ID') |
| *yes* | acme_certificate_aws_accesskey_secret  | an ec2 key secret | lookup('env', 'AWS_SECRET_ACCESS_KEY') |
| no | acme_certificate_group_members | certificate file group members | [] |
| no | acme_certificate_add_ca | add acme ca to the  | false |
| no | acme_certificate_directory | url to ca directory | https://acme-v01.api.letsencrypt.org/directory |
| no | acme_certificate_cafile (*) | symlink path to issuing ca cert file | _undefined_ |
| no | acme_certificate_intcafile (*) | symlink path to issuing intermediate ca cert file | _undefined_ |
| no | acme_certificate_certfile (*) | symlink path to cert file | _undefined_ |
| no | acme_certificate_chainfile (*) | symlink path to certificate chain file | _undefined_ |
| no | acme_certificate_keyfile (*) | symlink path to certificate key file | _undefined_ |

You can view an example redefinition of some of the above parameters, most notably the ones concerning certificate ca in the [CI test configuration file](/molecule/default/molecule.yml)

(*) useful for backwards compatibility with existing nginx/apache configurations

Please refer to the [defaults file](/defaults/main.yml) for an up to date list of input parameters.

## Dependencies

* [[geerlingguy.repo-epel](https://github.com/geerlingguy/ansible-role-repo-epel)]
* [[nephelaiio.plugins](https://github.com/nephelaiio/ansible-role-plugins)]
* [[nephelaiio.pip](https://github.com/nephelaiio/ansible-role-pip)]

See the [https://raw.githubusercontent.com/nephelaiio/ansible-role-requirements/master/requirements.txt](requirements) and [meta.yml](meta) files for more details

## Example Playbook

```
- hosts: servers
  vars:
    acme_certificate_email: ci@nephelai.io
    acme_certificate_domain: "{{ ansible_fqdn }}"
    acme_certificate_aws_accesskey_id: "{{ lookup('env', 'AWS_AK_ID') }}"
    acme_certificate_aws_accesskey_secret: "{{ lookup('env', 'AWS_AK_SECRET') }}"
  roles:
    - role: nephelaiio.acme-dnschallenge-route53
```

## Testing

Please make sure your environment has [docker](https://www.docker.com) installed in order to run role validation tests. Additional python dependencies are listed in the [requirements file](/requirements.txt)

Role is tested against the following distributions (docker images):
  * Ubuntu Xenial
  * CentOS 7
  * Debian Stretch

You can test the role directly from sources using command ` molecule test `

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
