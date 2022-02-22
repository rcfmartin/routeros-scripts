Upload backup to server
=======================

[◀ Go back to main README](../README.md)

> ℹ️ **Info**: This script can not be used on its own but requires the base
> installation. See [main README](../README.md) for details.

Description
-----------

This script uploads binary backup (`/ system backup save`) and complete
configuration export (`/ export terse`) to external server.

### Sample notification

![backup-upload notification](backup-upload.d/notification.svg)

Requirements and installation
-----------------------------

Just install the script:

    $ScriptInstallUpdate backup-upload;

Configuration
-------------

The configuration goes to `global-config-overlay`, these are the parameters:

* `BackupSendBinary`: whether to send binary backup
* `BackupSendExport`: whether to send configuration export
* `BackupPassword`: password to encrypt the backup with
* `BackupRandomDelay`: delay up to amount of seconds when run from scheduler
* `BackupUploadUrl`: url to upload to
* `BackupUploadUser`: username for server authentication
* `BackupUploadPass`: password for server authentication

Also notification settings are required for e-mail,
[matrix](mod/notification-matrix.md) and/or
[telegram](mod/notification-telegram.md).

### Issues with SFTP client

The RouterOS SFTP client is picky if it comes to authentication methods.
I had to disable all but password authentication on server side. For openssh
edit `/etc/ssh/sshd_config` and add a directive like this, changed for your
needs:

    Match User mikrotik
        AuthenticationMethods password

Usage and invocation
--------------------

Just run the script:

    / system script run backup-upload;

Creating a scheduler may be an option:

    / system scheduler add interval=1w name=backup-upload on-event="/ system script run backup-upload;" start-time=09:25:00;

See also
--------

* [Send backup via e-mail](backup-email.md)
* [Upload backup to Mikrotik cloud](backup-cloud.md)

---
[◀ Go back to main README](../README.md)  
[▲ Go back to top](#top)