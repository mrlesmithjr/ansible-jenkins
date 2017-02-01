Role Name
=========

Installs jenkins CI https://jenkins-ci.org/

Requirements
------------

None

Role Variables
--------------

````
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
````

Dependencies
------------

None

Example Playbook
----------------

#### GitHub
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-jenkins
  tasks:
````
#### Galaxy
````
---
- hosts: all
  become: true
  vars:
  roles:
    - role: mrlesmithjr.jenkins
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
