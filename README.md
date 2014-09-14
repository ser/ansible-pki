
## [![DebOps project](http://debops.org/images/debops-small.png)](http://debops.org) pki



[![Travis CI](http://img.shields.io/travis/debops/ansible-pki.svg?style=flat)](http://travis-ci.org/debops/ansible-pki) [![test-suite](http://img.shields.io/badge/test--suite-ansible--pki-blue.svg?style=flat)](https://github.com/debops/test-suite/tree/master/ansible-pki/)  [![Ansible Galaxy](http://img.shields.io/badge/galaxy-debops.pki-660198.svg?style=flat)](https://galaxy.ansible.com/list#/roles/1588) [![Platforms](http://img.shields.io/badge/platforms-debian%20|%20ubuntu-lightgrey.svg?style=flat)](#)






This role is meant to be a simple SSL certificate manager which:

  * creates self-signed certificate for a host, along with a CSR;
  * uploads the CSR for its certificate to Ansible Controller for easy
    signing by a CA;
  * downloads signed certificate from Ansible Controller when it becomes
    available;
  * downloads custom CA or wildcard certificates provided to the role by
    administrator in a specifc directory on Ansible Controller;

`debops.pki` role is planned to be rewritten to support automatic CA
signing and custom certificates for clients/applications.





### Installation

This role requires at least Ansible `v1.7.0`. To install it, run:

    ansible-galaxy install debops.pki

#### Are you using this as a standalone role without DebOps?

You may need to include missing roles from the [DebOps common
playbook](https://github.com/debops/debops-playbooks/blob/master/playbooks/common.yml)
into your playbook.

[Try DebOps now](https://github.com/debops/debops) for a complete solution to run your Debian-based infrastructure.





### Role dependencies

- `debops.secret`





### Role variables

List of default variables available in the inventory:

    ---
    
    # Should PKI be managed by Ansible
    pki: True
    
    # Copy wildcard certificates and keys to remote hosts?
    pki_wildcard: True
    
    pki_path: '/srv/pki'
    pki_private_group: 'ssl-cert'
    
    pki_digest: 'sha256'
    pki_bits: 2048
    pki_selfsign_days: 365
    
    # Default settings for new Certificate Requests
    pki_country:            'AA'
    pki_state:              '{{ ansible_domain | capitalize }} State'
    pki_locality:           '{{ ansible_domain | capitalize }} City'
    pki_organization:       '{{ ansible_domain | capitalize }} Organization'
    pki_organizationalUnit: '{{ ansible_domain | capitalize }} Department'
    pki_commonName:         '{{ ansible_fqdn }}'
    pki_email:              'root@{{ ansible_domain }}'
    
    # Default certificate for FQDN of a host
    pki_default_certificate:
      - cn: '{{ ansible_fqdn }}'
    
    # Example list of host certificates to create
    #pki_host_certificates:
    #  - cn: 'example.com'
    #    mail:
    #      - 'root@example.com'
    #    dns:
    #      - 'www.example.com'
    #      - 'mail.example.com'
    #      - '*.mail.example.com'
    #    uri:
    #      - 'http://example.com/'
    #    ip:
    #      - '192.0.2.1'
    #
    #  - cn: 'subdomain.{{ ansible_domain }}'
    #
    #  - cn: 'other.{{ ansible_domain }}'
    #    ou: 'Other Department'
    #    e: 'root@other.{{ ansible_domain }}'
    #    mail:
    #      - 'others@other.{{ ansible_domain }}'
    #      - 'root@{{ ansible_domain }}'
    #    dns:
    #      - '*.other.{{ ansible_domain }}'









### Authors and license

`pki` role was written by:

- Maciej Delmanowski | [e-mail](mailto:drybjed@gmail.com) | [Twitter](https://twitter.com/drybjed) | [GitHub](https://github.com/drybjed)

License: [GPLv3](https://tldrlegal.com/license/gnu-general-public-license-v3-%28gpl-3%29)



***

This role is part of the [DebOps](http://debops.org/) project. README generated by [ansigenome](https://github.com/nickjj/ansigenome/).