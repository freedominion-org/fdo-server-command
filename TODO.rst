fdo-server TODO list:
=====================


TODO
----

- ``file_server`` recipe needs looking at how to make better for multi-tenancy / multi-site. And the http_gateway-site.conf could be maybe be handled better, assuming user will change things after cooking.

DONE
----

- ``init-jails``: ``freebsd-update fetch`` when out of support window returns 1 which breaks failure check.
- Manage ``jail_parallel_start`` and ``jail_list`` in ``/etc/rc.conf``.
- ``"Enter the git user name"`` needs clarification.
- Improve global ``bashrc`` for unlimited, real-time, timestamped history.
- Fix ``TERM`` variable in bashrc for tmux to work preperly, it should change to ``screen``.
- Disable log rotation in host and jails. perhaps even all periodic.
- Convert reserved jail LAN IP addresses in rc.conf to only in ``jail.conf``.
- Make ``init-jails`` idempotent. TEST:(i) destroy when clones exist, (ii) rename of template fs.
- Do a ``check_configs`` in ``create-jail``.
- Move all (ldap) jail recipes syslog configuration from ``/etc/syslog.conf`` to individual ``/usr/local/etc/syslog.d/`` confs.
- Add ``"all checks passed"`` or ``"one or more failed"`` to end of ``check-configs``.
- Disable ``y`` prompts for installing packages in ``init-host``/``init-jails`` etc.
- Track template config files from ``create-jail`` to repo.
- Rename subcommand ``new-host`` to ``init-host``.
- ``init-host``: change ``sshd_config`` ``ListenAddress`` addditional line to a substition of the existing line.
- Create a script to add and remove ppp-nat/pf-nat port redirections and replace port forwarding variable substitutions.
- Jail recipes: use variable ``JAILS_LAN_SUBNET_C`` for ``JAIL_IP`` and other jail related IPs.
- All scripts: host/jail execution support and tests added or made consistent. (i) Exit with error if not run in host. (ii) Seemlessly work from inside or outside relevant jail.
- Change input confirmation prompt colours to make value stand out.
- Make a read inbuilt command replacement that supports password input and preset (suggested) text.
- Remove commented out entries from ``/etc/devfs.rules`` in ``init-host`` templates, replace with better sed to add entries.
- New subsystem: ``init-sshfs-daemon``: Make a subcommand to setup/enable ``sshfsd``
  (Requires: ``fusefs-sshfs`` package. ``fuse_load="YES"`` in ``loader.conf``. client key added to servers' ``authorized_keys``).
- Implement subcommand ``remove-config``.
- Add command usage entries for ``init-sshfs-daemon`` and ``remove_config``.
- Disable ``fetch_latest_self`` from scripts when calling ``fdo-server`` externally.
- Improve output and formatting for scripts; ``fdo-dns_cache|pf|ppp-list-*?*``.
- Move ``proceventd`` and ``notifierd`` back to scripts and fix ``service -e`` message.
- Copy ACL management scripts from beastie2@potensol.com and modify to suit fdo script coding style.
- Improve ``jlogin`` to allow better selection of similar named jails.
- Change template jail IP from 10.0.10.11 to 10.0.11.1.
- Change ``create-jail`` dataset creation from clone to send/recv.
- ``http_gateway``: disable upstreaming traffic of invalid/unused host names/IP addresses.
- All scripts which destroy filesystems should rename the backup pool filesystem, prefix with -DESTROYED (``fdo-hotdesk-remove-user``).
- Convert all exit codes to 1 for expected error, 2 for unexpected error and 3 for interupt error.
- Update all prompts and verification messages to new style (e.g. use single quotes and white on cyan text).
- ``fdo-backupz-thin-snapshots`` must ALWAYS keep the lastest TWO snapshots.
- ``fdo-backupz-thin-snapshots``, ``fdo-backupz-repair-state`` and ``fdo-backupz`` should both block one another.
- Jail recipes with additional filesystems should ask for pool to use (e.g. pxe recipe).
- ``fdo-pf|ppp-add|remove-port-forward-rule``: ask to reload service.
- ``update-config``: add checks for changes by using diff, before trying to commit.
- Replace tightvnc with tigervnc and ask for VNC screen size and password (see create_vm_template).
- ``init-vnc-desktop``: ask user for screen size from list of available.
- ``undo_*``: after install back previous repo configs, remove all config-templates files that did not exist before.
- ``init-host`` & ``init-vnc-desktop```: remove rc.local and rc.shutdown.local from config-templates, add to fdo-server.  
- ``init-host`` & ``init_jails``: remove /etc/syslogd.conf from config-templates, since it's no longer customised.
- ``init-host`` update newsyslog configs to FreeBSD 12.x layout.
- ``init-jails``: convert existing config-templates/init-jails folder to 'jail_template' and make init-jails for host configs.
- ``sshfsd`` rc script; change 'REQUIRE:' to "DAEMON FILESYSTEMS NETWORK netif" and add robustness to allow for slow network establishment.
- add template for ``/var/cron/tabs/root`` to ``init-host``.
- ``fdo-ppp-list-port-forward-rules`` ; add support for upper case (A-Z).
- script ``fdo-hotdesk-add-user``: use home folder ZFS quota variable from ``/usr/local/etc/fdo/hotdesk.conf``.
- ``init_local_repo``: better failure detection and handling.
- ``update_local_repo``: better failure detection and handling.
- ``init_git_config``: better failure detection and handling.
- ``upgrade_repo_from_upstream``: better failure detection and handling.
- ``check_repo_config``: better failure detection and handling.
- ``merge_local_repo_to_remote``: better failure detection and handling.
- Convert all config files to UCL.
- Make all sub-commands fully idempotent by adding more check and balances and cleanup function with trap interupt.
- `` config-templates``: split into per RELEASE directories.
- ``install_scripts_everywhere``: detect jails to install scripts to by checking for rc.conf.
- Convert sshfs-daemon connections config file to UCL ().
- Move rc.d scripts back to scripts instead of in config-templates.
- Archive old/unsupported ``remote-desktops`` subsystem configs/scripts.
- ``fdo-hotdesk-remove-user``: load backup pool from UCL host.conf file.
- hotdesk subsystem needs a list command/script ``fdo-hotdesk-list-users``.
- ``fdo-backupz-thin-snapshots``: change uclcmd to ${UCL_CMD}.
- ``fdo-dns_cache-add|remove-hostname``: don't ask user whether to update the repo with changes, just do it.
- ``patch_host``: always updare repo after successful patch.
- ``fdo-vms-start``: make sure tap interface gets added to bridge.
- ``fdo-vms-start``: add support for virtio-blk devices.
- ``fdo-vms-create-template|instance``: after eject,insert,detach,attach; ask whether to start vm.
- ``fdo-vms-create-template|instance``: add stop and start options in addition to restart.
- check diffs between FreeBSD-12.0-RELEASE and FreeBSD-12.1-RELEASE configs used in ``config-templates``.
- Add FreeBSD-12.2-RELEASE configs to ``config-templates``.
- Set all dialog menu loops to sleep for only 2 sec instead of 4.
- Convert all 'continue' prompts to 'proceed'.
- Make all dialog prompts use a DIALOG_PROMPT variable.
- Make all uses of ifconfig parsing more robust (e.g. grep -v " netmask 0xffffffff" and use spaces in greps).
- Make hotdesk subsystem store users in UCL config file, possibly along with their hashed passwords.
- ``create-vm-template``: add support for bhyve-grub and bhyveload.
- ``create-vm-template|instance``: add sanity test for subsystem initialisation.
- ``create-vm-template``: fix boolean bootable flag after attach image.
- ``jail-certs.list`` path (/jls/jailname/usr/local/etc/ssl/) needs reconsidering, since freebsd-update may not like it being there. Although it may be OK, since it's /usr/local/etc/ssl/certs/ that seems to be treated with respect. *EDIT* use /usr/local/etc/ssl/fdo-certs for all certs used by fdo-server.
