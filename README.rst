Slurm
-----

The Simple Linux Utility for Resource Management (Slurm) is an open
source, fault-tolerant, and highly scalable cluster management and job
scheduling system for large and small Linux clusters. `More
info. <http://www.schedmd.com/slurmdocs/slurm.html>`__

Install and configure slurm controller/master, worker, and database.

See the full `Salt formulas installation and usage
instructions <https://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html>`__

**Note:** Tested on CENTOS/RHEL 7 only. **Note:**
`Munge <http://dun.github.io/munge/>`__ is recommended & used in slurm
but Munge is it's own thing so you will also need a munge slurm state
that will implement munge in your environment. That should be pretty
easy, but for now I will leave it as an exercise for the user. Just note
this formula depends on Munge.

Available States
~~~~~~~~~~~~~~~~

-  `slurm <#slurm>`__
-  `slurm.build <#slurm.build>`__
-  `slurm.cgroups <#slurm.cgroups>`__
-  `slurm.config <#slurm.config>`__
-  `slurm.controller <#slurm.controller>`__
-  `slurm.login <#slurm.login>`__
-  `slurm.slurmdb <#slurm.slurmdb>`__
-  `slurm.spankX11 <#slurm.spankX11>`__
-  `slurm.worker <#slurm.worker>`__

slurm
^^^^^

Meta-state that adds config and installs slurm worker packages.

slurm.build
^^^^^^^^^^^

Install packages needed to build slurm rpms.

slurm.cgroups
^^^^^^^^^^^^^

Install base cgroups config. User will need to also add relevent config
to slurm.conf

slurm.config
^^^^^^^^^^^^

-  Create slurm user and group.
-  make ``/var/log/slurm`` folder
-  create master slurm.conf file ``/etc/slurm/slurm.conf``

slurm.controller
^^^^^^^^^^^^^^^^

Install slurmctld related packages, start service, create spool
directory, and add log file.

slurm.login
^^^^^^^^^^^

Include slurm.config and install other slurm packages so utilities are
available, but don't start any daemons.

slurm.slurmdb
^^^^^^^^^^^^^

-  Install slurmdbd and slurmsql packages, start services, create
   slurmdbd.conf, and add log file.
-  Create slurm accounting db

**Requires:** mariadb-server already be installed & mysql root password
in pillar.

slurm.spankX11
^^^^^^^^^^^^^^

Install slurm-spank-X11 and drop in config file.

slurm.worker
^^^^^^^^^^^^

Install slrumd worker packages, start service, create spool directory,
and add log file.
