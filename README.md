# Ansible Certificates
[![Build Status](https://travis-ci.org/supertarto/ansible-certificates.svg?branch=master)](https://travis-ci.org/supertarto/ansible-certificates)

Create self-signed certificates with Ansible.

## Requirements
None

## Tested plateform
* Debian 10 (Buster)

## Role variables
Boolean variables. Those are used to determine if we want to create our own CA, to create a self-signed certificate, and if we want to create a self-signed cert with our own CA.
```yml
cert_create_ca: false
cert_use_ownca: false
cert_use_self_signed: false
```
Information about our CA: Private Key, CSR, and Cert. 
```yml
cert_ca_private_key: []
# Exemple
#  - private_key_path: /etc/ssl/private/default_ca_key.key
#    size: 4096
#    type: RSA
#    owner: root
#    group: root

cert_ca_csr: []
# Exemple
#  - path: /etc/ssl/private/default_ca_csr.csr
#    private_key_path: /etc/ssl/private/default_ca_key.key
#    country_name: FR
#    organization_name: []
#    mail_address: []
#    common_name: []
#    owner: root
#    group: root
#    subject_alt_name: "IP:127.0.0.1"
#    basic_constraints:
#      - CA:TRUE

cert_ca_cert: []
# Exemple
#  - path: /etc/ssl/certs/default_ca_cert.crt
#    private_key_path: /etc/ssl/private/default_ca_key.key
#    csr_path: /etc/ssl/private/default_ca_csr.csr
#    owner: root
#    group: root
#    provider: selfsigned
```
Information about our Certificate: Private Key, CSR, and Cert. For the cert, if you want it to be signed by your own CA, you must define the **ca_path** and the **ca_privatekey_path**.
```yml
cert_private_key: []
# Exemple
#  - private_key_path: /etc/ssl/private/default_cert_key.key
#    size: 4096
#    type: RSA
#    owner: root
#    group: root

cert_csr: []
# Exemple
#  - path: /etc/ssl/private/default_cert_csr.csr
#    private_key_path: /etc/ssl/private/default_cert_key.key
#    country_name: FR
#    organization_name: []
#    mail_address: []
#    common_name: []
#    owner: root
#    group: root
#    subject_alt_name: "IP:127.0.0.1"
#    basic_constraints:
#      - CA:FALSE

cert_cert: []
# Exemple
#  - path: /etc/ssl/certs/default_cert.crt
#    private_key_path: /etc/ssl/private/default_cert_key.key
#    csr_path: /etc/ssl/private/default_cert_csr.csr
#    ca_path: "/etc/ssl/certs/default_ca_cert.crt"
#    ca_privatekey_path: "/etc/ssl/private/default_ca_key.key"
#    owner: root
#    group: root
#    provider: selfsigned
```

## Examples
```yml
  hosts: myhost
  roles:
    - role: supertarto.certificates
  vars:
    cert_use_self_signed: true  
    cert_private_key:
      - private_key_path: /etc/ssl/private/default_cert_key.key
        size: 4096
        type: RSA
        owner: root
        group: root

    cert_csr:
      - path: /etc/ssl/private/default_cert_csr.csr
        private_key_path: /etc/ssl/private/default_cert_key.key
        country_name: FR
        organization_name: []
        mail_address: []
        common_name: []
        owner: root
        group: root
        subject_alt_name: "IP:127.0.0.1"
        basic_constraints:
          - CA:FALSE

    cert_cert:
      - path: /etc/ssl/certs/default_cert.crt
        private_key_path: /etc/ssl/private/default_cert_key.key
        csr_path: /etc/ssl/private/default_cert_csr.csr
        owner: root
        group: root
        provider: selfsigned
```
## Installation
```
ansible-galaxy install supertarto.certificates
```
## License
GPL V3.0
