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

## Installing your development branch of RHODS Dashboard
* Copy `.env` to `.env.local`  
####
* Edit `.env.local`
  
        OC_URL=<your cluster api url>
        OC_USER=<admin user>
        OC_PASSWORD=<admin password>
        OC_PROJECT=redhat-ods-applications
        IMAGE_REPOSITORY=quay.io/<quay user>/odh-dashboard:<branch>
        SOURCE_REPOSITORY_URL=https://github.com/<repo>/odh-dashboard.git
        SOURCE_REPOSITORY_REF=<branch>
####
* Remove the `odh-dashboard` kustomizeConfig from the `opendatahub` `KfDef`
  - go to the developer perspective
  - Select the ‘redhat-ods-applications’ project
  - Search -> KfDef
  - Edit the yaml for `opendatahub` KfDef
  - Remove the section:

          - kustomizeConfig:
              overlays:
                - authentication
              repoRef:
                name: manifests
                path: odh-dashboard
            name: odh-dashboard
####
* Push your dashboard changes
####
* Run `make reinstall`

## Installing your development branch of RHODS Spawner UI
- Clone the `jsp-wrapper` repository

        git clone https://github.com/jeff-phillips-18/jsp-wrapper.git
- Create `.env.local`:

        QUAY_REPO=<your quay repo username>
        GIT_USER=<your git username>
        NAMESPACE=redhat-ods-applications
        OPERATOR_NAMESPACE=rhods-operator
        OPERATOR_NAMESPACE=redhat-ods-operator
        GIT_REF=<your branch>
        REMOTE_CMD=docker

- Push your changes to `jupyterhub-singleuser-profiles` to your branch
###
- From `jsp-wrapper`, run `make`
