fdo-server TODO list:
=====================


TODO
----

- Consider making a subcommand to setup/enable ``sshfsd`` (Requires: ``fusefs-sshfs`` package. ``fuse_load="YES"`` in ``loader.conf``. client key added to servers' ``authorized_keys``).
- Remote Desktops sub-system:

  - Remote Desktops should allow option for using VNC or RDP, perhaps choice made at ``init-remote-desktops`` stage.
  - ``create-remote-desktop-instance`` should add NAT port redirection to ``ppp.conf``/``pf.conf``.


DONE
----

- ``init-jails``: ``freebsd-update fetch`` when out of support window returns 1 which breaks failure check.
- Manage ``jail_parallel_start`` and ``jail_list`` in ``/etc/rc.conf``.
- ``"Enter the git user name"`` needs clarification.
- Improve global ``bashrc`` for unlimited, real-time, timestamped history, see Gentoo rollout.
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
