# Kubernetes DISA STIG


Configure a Kubernetes install to be DISA STIG compliant. All findings will be audited by default. Non-disruptive CAT I, CAT II, and CAT III findings will be corrected by default. Disruptive finding remediation can be enabled by setting `cntrk8stig_disruption_high` to `yes`.

This role is based on Kubernetes DISA STIG: [Version 1, Rel 6 released on  Jul 27, 2022](https://dl.dod.cyber.mil/wp-content/uploads/stigs/zip/U_Kubernetes_V1R6_STIG.zip).

## Join us

On our [Discord Server](https://discord.io/ansible-lockdown) to ask questions, discuss features, or just chat with other Ansible-Lockdown users

## Updating

Coming from a previous release.

As with all releases and updates, It is suggested to test and align controls.
This contains rewrites and ID reference changes as per STIG documentation.

## Auditing

There is no audit role for this benchmark at this time. Please keep checking back for the KUBERNETES-STIG-Audit repo. 

## Requirements

- Kubernetes 1.16.7 or higher - Other versions are not supported.

### General

- Basic knowledge of Ansible, below are some links to the Ansible documentation to help get started if you are unfamiliar with Ansible

  - [Main Ansible documentation page](https://docs.ansible.com)
  - [Ansible Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
  - [Tower User Guide](https://docs.ansible.com/ansible-tower/latest/html/userguide/index.html)
  - [Ansible Community Info](https://docs.ansible.com/ansible/latest/community/index.html)
- Functioning Ansible and/or Tower Installed, configured, and running. This includes all of the base Ansible/Tower configurations, needed packages installed, and infrastructure setup.
- Please read through the tasks in this role to gain an understanding of what each control is doing. Some of the tasks are disruptive and can have unintended consiquences in a live production system. Also familiarize yourself with the variables in the defaults/main.yml file or the [Main Variables Wiki Page](https://github.com/ansible-lockdown/KUBERNETES-STIG/wiki/Main-Variables).

## Documentation

- [Repo GitHub Page](https://ansible-lockdown.github.io/KUBERNETES-STIG/)
- [Getting Started](https://www.lockdownenterprise.com/docs/getting-started-with-lockdown)
- [Customizing Roles](https://www.lockdownenterprise.com/docs/customizing-lockdown-enterprise)
- [Per-Host Configuration](https://www.lockdownenterprise.com/docs/per-host-lockdown-enterprise-configuration)
- [Getting the Most Out of the Role](https://www.lockdownenterprise.com/docs/get-the-most-out-of-lockdown-enterprise)
- [Wiki](https://github.com/ansible-lockdown/KUBERNETES-STIG/wiki)

## Dependencies

The following packages must be installed on the controlling host/host where ansible is executed:

- python2-passlib (or just passlib, if using python3)
- python-lxml
- python-xmltodict
- python-jmespath

Package 'python-xmltodict' is required if you enable the OpenSCAP tool installation and run a report. Packages python(2)-passlib and python-jmespath are required for tasks with custom filters or modules. These are all required on the controller host that executes Ansible.

## Role Variables

This role is designed that the end user should not have to edit the tasks themselves. All customizing should be done via the defaults/main.yml file or with extra vars within the project, job, workflow, etc. These variables can be found [here](https://github.com/ansible-lockdown/KUBERNETES-STIG/wiki/Main-Variables) in the Main Variables Wiki page. All variables are listed there along with descriptions.

### Tags

There are many tags available for added control precision. Each control has it's own set of tags noting the control number as well as what parts of the system that control addresses.

Below is an example of the tag section from a control within this role. Using this example if you set your run to skip all controls with the tag ssh, this task will be skipped. The
opposite can also happen where you run only controls tagged with ssh.

```sh
tags:
    - CNTR-K8-010050
    - ssh
    - dod_logon_banner
```

## Branches

- **devel** - This is the default branch and the working development branch. Community pull requests will pull into this branch
- **main** - This is the release branch
- **reports** - This is a protected branch for our scoring reports, no code should ever go here
- **gh_pages** - github pages
- **all other branches** - Individual community member branches


## Community Contribution

We encourage you (the community) to contribute to this role. Please read the rules below.

- Your work is done in your own individual branch. Make sure to Signed-off and GPG sign all commits you intend to merge.
- All community Pull Requests are pulled into the devel branch
- Pull Requests into devel will confirm your commits have a GPG signature, Signed-off, and a functional test before being approved
- Once your changes are merged and a more detailed review is complete, an authorized member will merge your changes into the main branch for a new release.

## Pipeline Testing

uses:

- ansible-core 2.12
- ansible collections - pulls in the latest version based on requirements file
- runs the audit using the devel branch
- This is an automated test that occurs on pull requests into devel

## Support

This is a community project at its core and will be managed as such.

If you would are interested in dedicated support to assist or provide bespoke setups

- [Ansible Counselor](https://www.mindpointgroup.com/products/ansible-counselor-on-demand-ansible-services-and-consulting/)
- [Try us out](https://engage.mindpointgroup.com/try-ansible-counselor)
