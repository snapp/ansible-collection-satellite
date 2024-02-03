redhat.satellite.host_collections
=================================

This role defines Host Collections.

Role Variables
--------------

This role supports the [Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

- `satellite_host_collections`: List of host collections to create. Each host collection is represented as a dictionary which specifies the `name` of the host collection and an optional description assigned to the host collection. Optionally the host collection's state can be managed using `state`.

```yaml
satellite_host_collections:
  - name: Production-RHEL-8
    description: Red Hat Enterprise Linux (RHEL) 8 Production Patch Cycle and Service Level Agreement (SLA)
    state: present
  - name: Production-RHEL-9
    description: Red Hat Enterprise Linux (RHEL) 9 Production Patch Cycle and Service Level Agreement (SLA)
    state: present
  - name: Test-RHEL-8
    description: Red Hat Enterprise Linux (RHEL) 8 Test Patch Cycle and Service Level Agreement (SLA)
    state: present
  - name: Test-RHEL-9
    description: Red Hat Enterprise Linux (RHEL) 9 Test Patch Cycle and Service Level Agreement (SLA)
    state: present
```

Example Playbooks
-----------------

Create two host collections defined in the `satellite_host_collections` dictionary in ansible vars:

```yaml
- hosts: localhost
  roles:
    - role: redhat.satellite.host_collections
      vars:
        satellite_server_url: https://satellite.example.com
        satellite_username: "admin"
        satellite_password: "changeme"
        satellite_organization: "Default Organization"
        satellite_host_collections:
          - name: Production-RHEL-9
            description: Red Hat Enterprise Linux (RHEL) 9 Production Patch Cycle and Service Level Agreement (SLA)
            state: present
          - name: Test-RHEL-9
            description: Red Hat Enterprise Linux (RHEL) 9 Test Patch Cycle and Service Level Agreement (SLA)
            state: present
```
 
Create host collections defined in the `satellite_host_collections` dictionary in ansible vars:

```yaml
- hosts: localhost
  roles:
    - role: redhat.satellite.host_collections
      vars:
        satellite_server_url: https://satellite.example.com
        satellite_username: "admin"
        satellite_password: "changeme"
        satellite_organization: "Default Organization"
        satellite_host_collections: "{{ satellite_host_collections | map(attribute='name') | list }}"
```

The above example assumes that a yaml dictionary `satellite_host_collections` is already defined in Ansible variables. It uses yaml methods to select the name of each product from that dictionary, convert them all to a list, and pass that list to the definition of the host collection.
