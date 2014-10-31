# Vagrant-Windows
=================

## Launching Vagrant-Windows

  1. Install vagrant.
  2. Run vagrant up from this directory.

## Enable WinRM (For Ansible, etc...)

    1. Launch the box, create a new user called vagrant with password vagrant. Put this user in the Administrators group.
    2. Turn on WinRM:
        start an command line with Administrator privs.
        now run these commands in order:

```
 winrm quickconfig -q
 winrm set winrm/config/winrs @{MaxMemoryPerShellMB="512"}
 winrm set winrm/config @{MaxTimeoutms="1800000"}
 winrm set winrm/config/service @{AllowUnencrypted="true"}
 winrm set winrm/config/service/auth @{Basic="true"}
 sc config WinRM start= auto
```

