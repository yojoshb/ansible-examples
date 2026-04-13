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

```bash
# To list collections in a Execution Environment, simply run the container with the 'ansible-galaxy collection list' command

# Example
podman run registry.redhat.io/ansible-automation-platform-25/ee-supported-rhel9:latest ansible-galaxy collection list

# /usr/share/ansible/collections/ansible_collections
Collection                      Version     
------------------------------- ------------
amazon.aws                      9.2.0       
ansible.controller              4.6.14      
ansible.eda                     2.7.0       
ansible.hub                     1.0.0       
ansible.netcommon               7.1.0       
ansible.network                 4.0.0       
ansible.platform                2.5.20250604
ansible.posix                   1.5.4       
ansible.scm                     3.0.0       
ansible.security                3.0.0       
ansible.snmp                    3.0.0       
ansible.utils                   5.1.2       
ansible.windows                 2.7.0       
ansible.yang                    3.0.0       
arista.eos                      10.0.1      
cisco.asa                       6.0.0       
cisco.ios                       9.1.1       
cisco.iosxr                     10.3.0      
cisco.nxos                      9.3.0       
cloud.common                    4.0.0       
cloud.terraform                 3.0.0       
frr.frr                         2.0.2       
ibm.qradar                      4.0.0       
junipernetworks.junos           9.1.0       
kubernetes.core                 5.1.0       
microsoft.ad                    1.8.0       
openvswitch.openvswitch         2.1.1       
redhat.amq_broker               1.3.0       
redhat.amq_streams              1.0.0       
redhat.data_grid                1.3.1       
redhat.eap                      1.3.1       
redhat.insights                 1.3.0       
redhat.jbcs                     1.0.1       
redhat.jws                      2.0.0       
redhat.openshift                4.0.1       
redhat.openshift_virtualization 1.2.3       
redhat.redhat_csp_download      1.2.2       
redhat.rhbk                     2.2.2       
redhat.rhel_idm                 1.10.0      
redhat.rhel_system_roles        1.21.1      
redhat.rhv                      2.4.2       
redhat.runtimes_common          1.1.3       
redhat.sap_install              1.2.1       
redhat.satellite                3.10.0      
redhat.satellite_operations     1.3.0       
redhat.sso                      1.3.0       
sap.sap_operations              1.0.4       
servicenow.itsm                 2.6.3       
splunk.es                       4.0.0       
trendmicro.deepsec              4.0.0       
vmware.vmware                   1.10.1      
vmware.vmware_rest              4.6.0       
vyos.vyos                       4.0.2
```
