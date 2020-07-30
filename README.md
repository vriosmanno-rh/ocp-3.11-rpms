ocp-3.11-rpms
=========

Role to copy all required OCP 3.11 RPM repos from Red Hat to local disk for disconnected installation.

Requirements
------------

- Ansible >= 2.5
- RHEL == 7
- Active RHEL OpenShift 3.11 Subscription

Role Variables
--------------

| Parameter | Type | Required |  Default Value | Comments |
| --- | --- | --- | --- | --- |
| **rhsm_user** | string | yes | *undefined* | The account username with access to subscriptions on https://access.redhat.com |
| **rhsm_password** | string | yes | *undefined* | The account password with access to subscriptions on https://access.redhat.com |
| **rhsm_pool** | string | no | *undefined* | The subscription pool IDs to consume that contain OCP 3.11. (ex. `0123456789abcdef0123456789abcdef`) |
| **rhsm_unregister** | boolean | no | false | Unregister the system from RHSM when completed |
| **temp_sync_path** | string | yes | */tmp* | The temp path for the reposync files |

Role Tags
---------
| Tag | Comments |
| --- | --- |
| **cleanup** | Tag to run as last step to cleanup synced data stored in the `{{ temp_sync_path }}/rpms` |

Example Playbook
----------------

### Running with defaults
```yaml
- name: ocp-3.11-rpms example
  roles:
    - role: ocp-3.11-rpms
      tags:
        - repo-sync
      vars:
        rhsm_user: aPassword
        rhsm_password: auser@example.com
```

### Running with RHSM Pool ID defined
```yaml
- name: ocp-3.11-rpms example
  roles:
    - role: ocp-3.11-rpms
      tags:
        - repo-sync
      vars:
        rhsm_user: aPassword
        rhsm_password: auser@example.com
        rhsm_pool: 0123456789abcdef0123456789abcdef
```

### Running with specified sync paths
```yaml
- name: ocp-3.11-rpms example
  roles:
    - role: ocp-3.11-rpms
      tags:
        - repo-sync
      vars:
        content_sync_path: /data/sync
        rhsm_user: aPassword
        rhsm_password: auser@example.com
        temp_sync_path: /data/tmp
```

License
-------

GPLv3