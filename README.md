# oxide.one
Infrastructure relating to the management and maintenance of https://oxide.one

# Playbooks

## `create-syndicate.yaml`

Creates (and updates) a syndicate node.

Has no explicit dependencies on other services, as this will control the creation of those services.

Required variables:

- `DO_KEY`
- `CF_KEY`

