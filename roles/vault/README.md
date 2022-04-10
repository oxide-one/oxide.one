# Vault

This set of roles will help configure and manage Hashicorp Vault

# Requirements

None that I know of :3

# Shared Variables

These are variables that are shared amongst a number of these roles.


| Name                              | Optional      | Default               | Description           |
| ----                              | --------      | -------               | -----------           |
| `vault_token`                     | No            | "{{ lookup('ansible.builtin.env', 'HV_TOKEN') }}" | The token to login to vault with |
| `vault_url`                       | No            | "{{ lookup('ansible.builtin.env', 'HV_URL') }}" | The URL of vault |

# Roles

## certificate_authority

Create and mount a certificate authority within vault. Does nothing if the CA already exists.

Once the Certificate Authority is mounted, it will generate a root certificate and set the Issuing and Revocation URLS.

### Usage

```yaml
- name: "Setup Certificate Authorities for ETCD"
  ansible.builtin.include_role:
    name: "vault/certificate_authority"
  vars:
    vault_ca_description: "Basic stuff"
    component: "engine"
    state: "present"

    vault_root_cacert_common_name: etcd.gecko.oxide.one
    vault_ca_path: "gecko/etcd"
    vault_root_cacert_format: pem_bundle
    vault_root_cacert_key_type: rsa
    vault_root_cacert_organization: oxide.one
    vault_root_cacert_permitted_dns_domains: "sou.gecko.oxide.one,mmr.gecko.oxide.one"
    vault_root_cacert_private_key_format: der
    vault_root_cacert_ttl: 87600h
```
### Vars

| Name                              | Optional      | Default               | Description           |
| ----                              | --------      | -------               | -----------           |
| vault_ca_path                     | Yes           | "pki"                 | The path to mount the PKI engine to |
| vault_ca_description              | Yes           | "A cool vault"        | Description of engine |
| vault_ca_default_lease_ttl        | Yes           | "0s"                  | 
| vault_ca_max_lease_ttl: "87600h"
| vault_ca_force_no_cache: false
| vault_root_cacert_type "exported"
| vault_root_cacert_common_name "{{ dns_domain }}"
| vault_root_cacert_alt_names
| vault_root_cacert_ip_sans
| vault_root_cacert_uri_sans
| vault_root_cacert_other_sans
| vault_root_cacert_ttl "87600h"
| vault_root_cacert_format "pem_bundle"
| vault_root_cacert_private_key_format "der"
| vault_root_cacert_key_type "rsa"
| vault_root_cacert_key_bits
| vault_root_cacert_max_path_length
| vault_root_cacert_exclude_cn_from_sans
| vault_root_cacert_permitted_dns_domains
| vault_root_cacert_ou
| vault_root_cacert_organization
| vault_root_cacert_country
| vault_root_cacert_locality
| vault_root_cacert_province
| vault_root_cacert_street_address
| vault_root_cacert_postal_code 
| state                             | yes           | `"present"`           | State of the droplet. |
| do_droplet_region                 | yes           | `"lon1"`              | Slug name for the region that the droplet will be created in |
| do_droplet_size                   | yes           | `"s-1vcpu-1gb-amd"`   | The slug name for the size of the droplet |
| do_droplet_image                  | yes           | `""debian-11-x64""`   | The slug name for the Image of the droplet |
| do_droplet_ssh_key_fingerprint    | no            | `NONE`                | Your ssh key fingerprint. [Get from here](https://cloud.digitalocean.com/account/security) |
| do_droplet_project_name           | yes           | omitted               | The project name to store the droplet in |
| do_droplet_enable_ipv6            | yes           | `False`               | Enable IPV6 |
| do_droplet_enable_monitoring      | yes           | `True`                | Enable Monitoring |
| do_droplet_enable_backups         | yes           | `False`               | Enable Backups |
| do_droplet_tags                   | yes           | `NONE`                | List of tags to apply to the droplet |