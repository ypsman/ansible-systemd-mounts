systemd mounts
==============
[![Build Status](https://travis-ci.org/ypsman/ansible-systemd-mounts.svg?branch=master)](https://travis-ci.org/ypsman/ansible-systemd-mounts)

Setup mounts as sysemd Service.

This Playbook creates a Systemd Service for mounting Shares.

So you can use mounts as system Servie.

Works for debian stretch, and Jessie if you use systemd.

for Example:
    
    systemctl status mount-point.mount
    systemctl start mount-point.mount
    systemctl stop mount-point.mount


Options:
--------

    Appdir:                           # description of the Service
    share: //apps.local/apps$         # Share to mount from
    mount: /opt/app                   # Folder to mount in
    type: nfs                         # mount type (look at mount man page)
    options: uid=1000                 # Options, username...
    automount: false                  # If false: the service will mount at boot
                                      # if true: Mount when access on the Folder and on boot


Example Playbook
----------------

    - hosts: all
      roles:
        - role: systemd-mounts
          mounts:
            myLogDir:
              share: //logserver.local/logs$
              mount: /mnt/logs
              type: cifs
              options: domain=local,username=user,password=password,uid=1000,gid=1000
              automount: true
            Appdir:
              share: //apps.local/apps$
              mount: /opt/app
              type: nfs
              options: uid=1000
              automount: false
