# Digitalocean

This set of roles will help configure and manage Digitalocean related 'things'

# Requirements

```bash
ansible-galaxy collection install community.digitalocean
```


# Roles

## droplet (Manage Droplets)

This is a hilariously simple module that will allow you to create droplets fairly easily.

It'll create a droplet based on the inventory hostname.

Once the Droplet is created, it will fetch the IPV4 information and set it as the `ansible_host` so you can SSH into it.

The ideal workflow would be to create a node to immeadietely work on it. Bear in mind that you should use a local connection until the node is created.

### Usage

```yaml
- name: "Create a node on DigitalOcean"
  hosts: do_node
  connection: local
  tasks:
    - ansible.builtin.import_role:
        name: digitalocean/droplet
      vars:
        state: present
```
 
### Required ENV Vars

`DO_KEY` - Your DigitalOcean API key

### Vars

| Name                              | Optional      | Default               | Description           |
| ----                              | --------      | -------               | -----------           |
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