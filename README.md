Ansible Role - Doas
=========

Ansible role to replace sudo with OpenDoas.

Install from Ansible Galaxy using this command: ansible-galaxy install dandyrow.doas

View Ansible Galaxy page [here](https://galaxy.ansible.com/dandyrow/doas).

This role uninstalls sudo after it checks to make sure the syntax of doas.conf is correct. I am not responsible if you get locked out of root privileges due to a mistake you made in the contents of the doas conf file. Sudo will not be uninstalled if the syntax is incorrect in doas.conf.

Currently only supported on arch, use on other distros at your own risk. May add support for other distros in the future.

Role Variables
--------------

The following variables can be found in defaults/main.yml. If their defaults are not to your preference change them when calling the role as shown in the example playbook below.

`doas_conf: [ permit :wheel ]` - Array of lines to insert into doas.conf to configure doas. See [doas.conf(5)](https://man.archlinux.org/man/doas.conf.5) manpage for guidance on how to configure doas.

`uninstall_sudo: true` - Whether to uninstall sudo after doas is installed and it's configuration is verified.

`delete_sudoers: true` - Whether to delete the sudoers file which is the configuration file for sudo.

The following variables can be found in vars/main.yml. They contain variables which do not need to be changed by the user unless the role is being used in an unsupported distro.

`doas_package: opendoas` - Package name for doas.

`doas_conf_file: /etc/doas.conf` - Configuration file for doas.

`sudo_package: sudo` - Package name for sudo.

`sudoers_file: /etc/sudoers` - Configuration file for sudo.

Supported Platforms
-------------------

* Arch Linux

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
    - name: Replace sudo with doas keeping sudoers file
      hosts: all
      roles:
        - role: doas
          vars:
            doas_conf:
              - permit arthur
              - deny joe
              - permit persist :wheel
            delete_sudoers: false
```

License
-------

GPL-3.0-only

Contributing
------------

To contribute to the project please fork it, make your changes then open a pull request. Your changes will be considered for merging provided it passes all CI tests. If any changes are required before merging these will be discussed in the pull request discussion thread.

Author Information
------------------

Created by Daniel Lowry (dandyrow). 

Email: [development@daniellowry.co.uk](mailto:development@daniellowry.co.uk)
