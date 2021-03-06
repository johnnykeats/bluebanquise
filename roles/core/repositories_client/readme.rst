Repositories client
-------------------

Description
^^^^^^^^^^^

This role simply configure repositories for client hosts.

CentOS
""""""

Since the content of the ISO DVD is copied in the os/ directory of the
repository server, this role disable CentOS default repositories.

For CentOS 7, all repositories *base*, *updates* and *extras* are disabled and
replaced by the *os* repo.

For CentOS 8, instead of disabling the default OS repositories *BaseOS* and
*AppStream*, the role will update the repo configuration to use paths
*.../os/BaseOS/* and *.../os/AppStream/*. The role still disables the *Extras*
repository which is enabled by default but not shipped with the ISO DVD. If one
need to add the *Extras* repo, it is advised to add it to the inventory like
any other repository.

.. code-block:: yaml

  repositories:
    - Extras
    - bluebanquise
    - os

There is a use case of people running CentOS 7 with a local clone of the *base*
repository but still using the online *updates* repository. You can keep this
behaviour by adding this repo to the external_repositories parameter in your
inventory. Please consider using the mirror closest to your location.

.. code-block:: yaml

  external_repositories:
    - name: "CentOS-Updates"
      baseurl: "http://mirror.centos.org/centos/7/updates/x86_64/"
      gpgcheck: 1
      gpgkey: "file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7"

Note that the `update repository does not exist anymore in CentOS 8
<https://wiki.centos.org/FAQ/CentOS8#I_don.27t_see_the_updates_repo_for_CentOS-8>`_.

Instructions
^^^^^^^^^^^^

See repositories_server role instructions for more details.

To be done
^^^^^^^^^^

Need to clear up the Ubuntu repositories process, still not clear how to handle
own made repos and officials repos as Ubuntu add local repos everywhere in the
sources.list file.

Changelog
^^^^^^^^^

* 1.0.3: Add support of major release version. Bruno <devel@travouillon.fr>
* 1.0.2: Added Ubuntu 18.04 compatibility. johnnykeats <johnny.keats@outlook.com>
* 1.0.1: Documentation. johnnykeats <johnny.keats@outlook.com>
* 1.0.0: Role creation. Benoit Leveugle <benoit.leveugle@gmail.com>
 
