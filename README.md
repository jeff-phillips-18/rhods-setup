# rhods-setup

Clone this repository
```
git clone https://github.com/jeff-phillips-18/rhods-setup.git
```
Clone the `olminstall` repository (must be on the VPN)
```
git clone https://gitlab.cee.redhat.com/croberts/olminstall.git
```

## Installing RHODS on a development cluster

- OC login to your cluster as kubeadmin
  `oc login <cluster API url> -u kubeadmin -p <kubeadmin password>`
####
- Update the machine set counts
  `scripts update-machine-sets`
####
- Wait for machine sets to finish updating (Compute -> Machine Sets in Console / Admin)
####
- Run the RHODS setup script
  `<path to olminstall directory>/setup.sh`  
####
- Create the rhodsadmin user
  `scripts/create-rhods-admin`  
  wait a minute or two and perform the login command give
####
- Login to the Console using the rhodsadmin user (rhodsadmin/rhodsadmin)
####
- Navigate to Topology in the `redhat-ods-applications`
####
- Launch the RHODS Dashboard from the `odh-dashboard` node
####
- Launch the Spawner UI from the `jupyterhub` node
