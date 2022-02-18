# Cloudflare

This set of roles will help configure and manage Cloudflare stuff (primarily DNS records)

# Requirements

```bash
ansible-galaxy collection install community.general
```

# Roles

## dns_record (Manage DNS records)

It'll create a dns record based on the parameters you give it.

By default, it'll just add a record to match your Cloudflare Inventory hostname to it's IP address

### Usage

```yaml
    - ansible.builtin.import_role:
        name: cloudflare/dns_record
      vars:
        state: present
```
 
### Required ENV Vars

`CF_KEY` - Your Cloudflare API key

### Vars

| Name                              | Optional      | Default                               | Description           |
| ----                              | --------      | -------                               | -----------           |
| state                             | yes           | `"present"`                           | State of the Record.  |
| dns_cf_zone                       | no            | `NONE`                                | The zone              |
| dns_cf_record                     | yes           | `"{{ inventory_hostname_short }}"`    | The record            |
| dns_cf_type                       | yes           | `"A"`                                 | Record Type           |
| dns_cf_value                      | no            | `"{{ ansible_host }}"`                | Value of the record   |
