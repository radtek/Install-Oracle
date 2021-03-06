#==============================================================================
#       (c) Copyright 2004 Hewlett-Packard Development Company, L.P.
#    The information contained herein is subject to change without notice.
#==============================================================================
#

HPE Install Oracle -
====================

Object:
--------
This package goal is to provide a set of scripts to install Oracle 12c Single Instance on a REDHAT 6 or 7 environment. 
It does use the silent install mode in order to create the ORACLE_HOME and to create a database.

Restriction:
------------
These scripts were tested for the deployment of multiple single instances (up to 12) in parallel on several nodes. However, it was not tested for a RAC deployment. This might work when the rsp files are updated accordingly.

Installation procedure:
-----------------------
1/ rsfo need to be run before running this package. rsfo takes care of the system prerequisites. For more information about rsfo, please visit:
https://github.com/yannallandit/rsfo

2/ ssh need to be enabled between all nodes including the local. If rsfo was used, this is already done

3/ The Oracle distribution need to be presented via nfs. 
The NFS configuration should be done this way:
3.1/ On the NFS server:
   # more /etc/exports
   /kits   *(async,no_root_squash)
   # systemctl restart nfs-config
   # systemctl restart nfs
3.2/ The Oracle installation files need to be located in a NFS directory. Or instance /kits/oradb/
   # ls /kits/oradb/
   install  response  rpm  runInstaller  sshsetup  stage  welcome.html
3.3/ On all the clients where Oracle will be installed:
   # mkdir /kits
   # mount -t nfs rsfodev:/kits /kits

4/ Run ./DeployOracle.sh

Silent installation:
--------------------
In order to perform an installation without user interaction, you need, before s
tarting the procedure to setup the configuration files as describe below:
1/ Copy the rsfoparam.txt & the nod_list.txt files in /tmp/scripts/

2/ update the nod_list.txt by adding the list of nodes where rsfo will run. Incl
ude the nodes name reachable by ssh without password.

3/ Update the rsfoparam.txt with the accurate parameters.

Scripts:
--------

1/ DeployOracle.sh: Is the scripts to be used in order to deploy Oracle.

2/ InstO.sh: is called by DeployOracle.sh and manage the various steps of the Oracle installation

3/ db_install.rsp: Is the response file for the Oracle binaries installation. This file can be modified based on your Oracle requirements

4/ dbca.rsp: Is the response file for the database creation. Here also, can be modified in order to align the db design with the needs.

Contacts:
---------
Send your questions or comments to yann.allandit@hpe.com.

