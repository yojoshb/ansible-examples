## Utilizing the `microsoft.ad.ldap` inventory plugin to create a dynamic ansible host inventory

[microsoft.ad.ldap inventory plugin](https://docs.ansible.com/projects/ansible/latest/collections/microsoft/ad/ldap_inventory.html)

- `microsoft.ad.ldap.yml`: Inventory file to place into your project
- `input_config.yml`: Custom Credential Input Configuration
- `injector_config.yml`: Custom Credential Injector Configuration

### Configuration
1. Create a custom credential type.
Use [input_config.yml](./input_config.yml) and [injector_config.yml](./injector_config.yml) for values.

2. Create a credential using the credential type from step 1.

3. Add an inventory file to your project using the microsoft.ad.ldap plugin. You can use the example [microsoft.ad.ldap.yml](./microsoft.ad.ldap.yml) and modify to your needs.

4. Create an inventory and inventory source using the project and microsoft.ad.ldap.yml inventory file.

5. Sync the inventory and verify hosts are added.
