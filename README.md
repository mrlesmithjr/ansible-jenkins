<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-jenkins](#ansible-jenkins)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [Vagrant Usage](#vagrant-usage)
    - [Spinning up Vagrant test environment](#spinning-up-vagrant-test-environment)
  - [Tearing down Vagrant test environment](#tearing-down-vagrant-test-environment)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-jenkins

An [Ansible](https://www.ansible.com) Role to Install/Configure [Jenkins CI](https://jenkins-ci.org/)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-jenkins
config_jenkins: false  #defines if jenkins will be configured from templates or left as default install
enable_jenkins_sudo: false  #defines if jenkins user should have sudo rights (Useful for running Ansible tasks from CLI)
install_tower_cli: false  #defines if ansible tower cli should be installed
jenkins_ansible_info:
  name: 'Default'
  home: '/usr/local/bin'
jenkins_apt_repo: 'deb http://pkg.jenkins-ci.org/debian binary/'
jenkins_cli_path: '{{ jenkins_home_dir }}/jenkins-cli.jar'
jenkins_config_info:
  num_executors: 2
  use_security: true
  auth_strategy: 'AuthorizationStrategy$Unsecured'  #AuthorizationStrategy$Unsecured or FullControlOnceLoggedInAuthorizationStrategy
  disable_remember_me: false
  system_message: 'Welcome to the Jenkins lab'
jenkins_debian_pre_req_packages:
  - 'default-jdk'
  - 'default-jre-headless'
  - 'jenkins'
jenkins_email_info:
  default_suffix: '@{{ pri_domain_name }}'
  reply_to_address: 'jenkins@{{ pri_domain_name }}'
  smtp_host: 'smtp.{{ pri_domain_name }}'
  use_ssl: false
  smtp_port: 25
jenkins_home_dir: '/var/lib/jenkins'
jenkins_ldap_info:
  active_directory: true
  enabled: false
  server: '192.168.202.200'
  port: 389
  root_dn: 'DC=example,DC=org'
  user_search_base: 'CN=Users'
  manager_dn: 'CN=gitlab,CN=Users,DC=example,DC=org'
  manager_password: 'P@55w0rd'  #This will be encrypted when saved from WebUI
  disable_email_address_resolver: false
jenkins_manage_plugins: false  #Defines if plugins will be managed using Ansible...
jenkins_plugins:
  - 'active-directory'
  - 'ansible'
  - 'build-pipeline-plugin'
  - 'git'
  - 'gitlab-plugin'
  - 'job-dsl'
  - 'ldap'
  - 'logstash'
  - 'PowerShell'
  - 'rundeck'
  - 'ssh'
  - 'travis-yml'
  - 'vagrant'
  - 'vmware-vrealize-automation-plugin'
  - 'vmware-vrealize-codestream'
  - 'vsphere-cloud'
  - 'workflow-aggregator'
jenkins_redhat_pre_req_packages:
  - 'java-1.7.0-openjdk'
jenkins_repo_key: 'http://pkg.jenkins-ci.org/{{ ansible_os_family|lower }}/jenkins-ci.org.key'
pri_domain_name: 'example.org'
```

## Dependencies

None

## Example Playbook

```yaml
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-jenkins
  tasks:
```

## Vagrant Usage

Included is a [Vagrant](https://www.vagrantup.com) test environment to easily
spinup. This environment is very useful for quickly spinning up a usable
[Jenkins CI](https://jenkins-ci.org/) platform. It is also very useful for
learning how to provision a [Jenkins CI](https://jenkins-ci.org/) platform using
[Ansible](https://www.ansible.com).

### Spinning up Vagrant test environment

To spin up this test environment simply execute:

```bash
cd Vagrant
vagrant up
```

Once the provisioning is complete you can then connect to the
[Jenkins WebUI](http://192.168.250.10:8080) using your browser of choice and
begin doing some cool stuff.

> NOTE: This setup is an insecure setup without any authentication enabled
> and it should be treated as purely a playground.

## Tearing down Vagrant test environment

Once you are done using this test environment and are ready to tear it all down
simply execute:

```bash
cd Vagrant
./cleanup.sh
```

## License

BSD

## Author Information

Larry Smith Jr.

-   [@mrlesmithjr](https://www.twitter.com/mrlesmithjr)
-   [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
-   mrlesmithjr [at] gmail.com
