## AAP Configuration as Code (CaC) Example

- Example was used to export AAP 2.6 containerized data into a AAP 2.7 OpenShift Operator deployment
- Uses the current collections `aap_configuration-4.9.0` and `aap_configuration_extended-4.9.1` 
    - Check `requirements.yml` for all needed collections
    - https://console.redhat.com/ansible/automation-hub/collections/validated/infra/aap_configuration/details
    - https://console.redhat.com/ansible/automation-hub/collections/validated/infra/aap_configuration_extended/details
- Upstream docs: https://github.com/redhat-cop/aap_configuration_extended and https://github.com/redhat-cop/infra.aap_configuration

### Environment setup
Credentials/API Tokens can be setup multiple ways. You can use the upstream docs format to create and destroy a token on use in the playbooks, using username/password for initial connection. This example uses a pre-generated token, and stores it in `group_vars` with a vaulted token for each instance
```bash
group_vars/
├── containerized
│   ├── connection.yml
│   └── vault.yml
└── openshift
    ├── connection.yml
    └── vault.yml
```

### Export and Import
Basic playbooks included `export_aap.yml` and `import_aap.yml`

> Note:  `aap_configuration_extended v4.10.0` simplifies the import process with not having to deal with structured exports so strictly. Importing currently needs a much more verbose playbook if you're not using the original hierarchical CaC defaults `(…/env/common/…)`.
> https://github.com/redhat-cop/aap_configuration_extended/tree/4.10.0/roles/filetree_read#roundtrip-from-filetree_create

- This example  use tags to select certain AAP objects to be exported and imported. You can omit the tags, and perform the operations over the entire AAP instance if wanted. You can view available tags like so:
```bash
ansible-playbook export_aap.yml --list-tags
```

- Export AAP Configuration:
```bash
ansible-playbook export_aap.yml -i inventory.yml -e @group_vars/containerized/vault.yml --ask-vault-pass
```

- Import AAP Configuration:
```bash
ansible-playbook import_aap.yml -i inventory.yml -e @group_vars/openshift/vault.yml --ask-vault-pass
```

### Secrets as variables
You cannot directly export sensitive data from the AAP API. The export role includes `secrets_as_variables`, a way to set sensitive data as variables, allowing importing using a vars file. Make sure to Vault this file.

- Here's a quickish way to create a credentials vars file from an export. It will go through the exported tree `./filetree_export`, find all *secrets_as_variables* as they always start with `vaulted_`, then dump them to `./filetree_export/secrets_vars.yml` with the values set to `CHANGE_ME`
```bash
grep -rhoE '\{\{[[:space:]]*vaulted_[A-Za-z0-9_]+[[:space:]]*\}\}' ./filetree_export | sed -E 's/^\{\{[[:space:]]*//; s/[[:space:]]*\}\}$/: CHANGE_ME/' | sort -u > ./filetree_export/secrets_vars.yml
```

- Simply edit the `secrets_vars.yml` file, and change the values accordingly, and vault the file

- Some templated objects may not get caught from the read operation i.e. `gateway_authenticators.yaml`. You may have to manually edit these files and add a variable to reference in your `secrets_vars.yml` 

- SSH Key variables should layout like so: 
```yaml
vaulted_controller_credentials_gitlab_ssh_key_data: |
  -----BEGIN OPENSSH PRIVATE KEY-----
  b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
  d64oJ/YLbcMsbA1TL10T3MXbCt2zVhiVrTQ3v09xfYB0hRHqvKX+05UONRKbPvT8vRJfUX
  ...
  ...
  -----END OPENSSH PRIVATE KEY-----  
```

- `aap_configuration_extended v4.10.0` simplifies this and creates the file for you: https://github.com/redhat-cop/aap_configuration_extended/tree/4.10.0/roles/filetree_create#usage-example-for-the-secrets_as_variables-feature
