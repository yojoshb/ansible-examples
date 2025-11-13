## Utilizing the `ansible.scm` module in an ansible execution environment

AAP standard `ee-supported-rhel9` & `ee-supported-rhel8` comes out-of-the-box with various modules pre-installed. `ansible-scm` can be used to pull/push to remote repositories from the EE.

> [!NOTE]
> The `ansible.scm` module utilizes repository tokens and not SSH keys currently. Create a token for your user account on your SCM platform and utilize it in the playbook 

- `inventory/hosts`: Basic host inventory
- `playbooks/scm-example.yaml`: Basic playbook to clone a GitHub/GitLab repository to the EE (localhost), fetch a remote file, then commit and push the fetched file to the repository

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
