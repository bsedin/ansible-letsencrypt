# ansible-letsencrypt
Ansible role to retrieve SSL certificates with letsencrypt

Create `./library` directory in your ansible project:

```
mkdir ./library
```

And configure `ansible.cfg`:

```
[defaults]
roles_path = ./library
```

Add submodule:

```
git submodule add git@github.com:kressh/ansible-letsencrypt.git library/letsencrypt
```

Use role:

```yaml
---
- hosts: lb01.yourserver.io
  remote_user: ansible
  become: true
  vars:
    letsencrypt_account_email: postmaster@yourdomain.io
    letsencrypt_account_key_content: |
      -----BEGIN RSA PRIVATE KEY-----
      <your letsencrypt key content>
      -----END RSA PRIVATE KEY-----
    letsencrypt_acme_directory: https://acme-staging.api.letsencrypt.org/directory # Use https://acme-v01.api.letsencrypt.org/directory in production
    letsencrypt_csr_email: support@yourdomain.io
    letsencrypt_csr_country: UK
    letsencrypt_csr_organization: Yourdomain Ltd.
    letsencrypt_domains:
      - fqdn: yourserver.io
      - fqdn: subdomain.yourserver.io
        private_key_size: 4096
        organization: Your Another Organization Ltd.
        email: postmaster@youranotherserver.io
        country: UK
  roles:
    - letsencrypt
```

See also: https://github.com/kressh/ansible-ssl-sync
