# Cacerts Import

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-cacerts-import.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-cacerts-import)

Import a Certificate into the cacerts certificate authority.

## Role Variables

`cacerts` is the only variable required. It takes a location either local
or remote.

For a local we need the folder the certificate is in and the certificates name.
Along with the alias.

For a Remote Certificate you need a name of the certificate, the alias
of the certificate, the remote server to retrieve it from and the port to
find it at. By default port is 443.


```yaml
# java_home is expected to be provided.
#

cacerts_remote_cert_location: /etc/ssl/certs
cacerts_remote_cert_owner: root
cacerts_remote_cert_group: root

cacerts_store_pass: changeit


# cacerts:
#   - location: local
#     name: certname.pem
#     folder: path
#     alias: certalias
#   - location: remote
#     name: certname.pem
#     alias:
#     server:
#     port: port
```

## Example Playbook

```yaml
- hosts: yourhostname
  become: yes
  vars:
    cacerts:
      - name: Identity.pem
        alias: Identity
        location: remote
        server: identity.test.school.edu
        port: "443"
  roles:
    - ChristopherDavenport.cacerts-import
```
