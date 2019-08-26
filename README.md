Composer Update
===============

Takes a [Composer](https://en.wikipedia.org/wiki/Composer_(software))-based [Git](https://en.wikipedia.org/wiki/Git) repository branch, updates it, and then pushes to the same (or another) branch.

Overview
--------

This Ansible role does the following:

1. Clones the Git repository to a temporary directory.
1. Switches to a different branch (if necessary).
1. Runs Composer's update command.
1. Commits `composer.lock`.
1. Pushes the commit to the specified (or same) branch.

Requirements
------------

The below requirements are needed on the host that executes this module.

* PHP
* Composer installed in bin path (recommended `/usr/local/bin`)
* Git version >= 1.7.1 (the command line tool)

Role Variables
--------------

See [defaults/main.yml](https://gitlab.com/consensus.enterprises/ansible-roles/ansible-role-composer-update/blob/master/defaults/main.yml).

Dependencies
------------

None.

Possible Enhancements
---------------------

* Currently, this role always clones to a new temporary directory.  It might make sense to use reuse an existing clone, but then things get more complicated as the working tree could be dirty.  So additional work would be required to check for and handle that.  As usual, merge requests are welcome.

Example Playbook
----------------

```yml
- hosts: dev.example.com
  roles:
    - consensus.composer-update
  vars:
    composer_update_git_url: "git@gitlab.com:example/myproject.git"
    composer_update_git_clone_branch: "master"
    composer_update_git_push_branch: "dev"
    composer_update_packages: "foo/bar foo/baz"
```

Testing
-------

Tests can be run like so (with more or fewer "v"s for verbosity):

```sh
ansible-playbook -vv --inventory TARGET_HOSTNAME, /path/to/this/role/tests/TEST_NAME.yml
```

Feel free to add your own tests in `tests/`, using existing ones as examples.  Contributions welcome.

Issue Tracking
--------------

For bugs, feature requests, etc., please visit the [issue tracker](https://gitlab.com/consensus.enterprises/ansible-roles/ansible-role-composer-update/-/boards).

License
-------

[AGPLv3](https://en.wikipedia.org/wiki/Affero_General_Public_License)

Author Information
------------------

Written by [Colan Schwartz](https://consensus.enterprises/team/colan/) and other folks at [Consensus Enterprises](https://consensus.enterprises/).  To contact us, please use our [Web contact form](https://consensus.enterprises/#contact).
