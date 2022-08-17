# OpenFlight Ansible Playbook

## Using the Playbook

- Install Ansible
    ```shell
	yum install -y ansible
	```
- Clone the playbook
    ```shell
	git clone https://github.com/openflighthpc/openflight-ansible-playbook/
	```
- Navigate to ansible directory
    ```shell
	cd openflight-ansible-playbook
	```
- Create inventory file called something sensible (e.g. `mycluster.inv`) with the following content (ensure hostnames are correct to what you have created)
    ```shell
	[head]
	clogin1

	[nodes]
	cnode01
    cnode02
    cnode03
	```
- Open `group_vars/all` for editing and...
	- Set `cluster_name` to your chosen cluster name
	- Set `compute_ip_range` to the IPv4 CIDR block chosen for the VPC
- Run the playbook
    ```shell
	ansible-playbook -i mycluster.inv main.yml
	```

### Excluding Particular Roles

The playbook is written in such a way that certain configuration steps can be avoided. For example, the underlying systems have a complex NFS server configuration so the research environment won't need a simple NFS server setup. This can be avoided by specifying the `--extra-vars` argument as follows:
    ```shell
    ansible-playbook -i mycluster.inv --extra-vars "nfs-server=false" main.yml 
    ```

Note that the above will still setup NFS client configuration for the mountpoints defined in `group_vars/all`. This allows for the playbook to integrate with existing NFS servers if needs be. 

## Versioning

The version release tags align with the tags in the openflight-compute-cluster-builder tags.
