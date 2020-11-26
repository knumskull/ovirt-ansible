# ovirt-ansible
Collection of ansible snippets for oVirt/RHV


## Create hosted-engine deployment hook for [Red Hat Solution 4088711](https://access.redhat.com/solutions/4088711)

### configure `config/rhv-m.yml` to setup credentials for RHV-Manager environment
The following configuration example is the minimum required to run this script.

```
engine_url: "https://rhv-m.example.com/ovirt-engine/api"
engine_user: admin@internal
engine_password: redhat01
engine_cafile: /etc/pki/ovirt-engine/ca.pem
```

### Using the playbook
To run this playbook, a host with `ansible >= 2.7` and `ovirt-engine-sdk-python >= 4.4.0` and [ovirt.ovirt](https://galaxy.ansible.com/ovirt/ovirt) Collection installed is required. 

Once available, a simple clone of git repository and execution of the playbook `create-fix_network-hook.yml` is needed to get create the hook.

```
$ git clone https://github.com/knumskull/ovirt-ansible.git
$ cd ovirt-ansible
$ ansible-playbook create-fix_network-hook.yml


### Example Output of fix_network.yml
This is an example output of running this playbook to be used in correct location described in [Red Hat Solution 4088711](https://access.redhat.com/solutions/4088711).

```
- include_tasks: auth_sso.yml
- name: Wait for the engine to reach a stable condition
  wait_for: timeout=300
- name: fix network
  ovirt_network:
     auth: "{{ ovirt_auth }}"
     name: "{{ item }}"
     data_center: Default
     clusters:
        - name: Default
          required: False
  with_items:
       - storage
 ```


# Disclaimer
There is no warranty on success by using these scripts. You will use these scripts on your own risk.
