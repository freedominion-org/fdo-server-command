fdo-server BUGS list:
=====================


BUGS
----

*Currently there are no known bugs*


FIXED
-----

- At the end of upgrade-repo-from-upstream we get "But we were unable to push changes to the private remote repo." when we are a local only repo.
- After fail jail creation (ldap_consumer, dhcp_server) and auto-revert, the host has stale /etc/fstab.jail_name in local repo configss/ dir.
- ``setup-vnc-desktop``: make rc.local and rc.shutdown.local preparation more robust.
- ``setup-vnc-desktop``: init-host needs to add LAN IP and hostname (FQHN, same as 'hostname' command output) to /etc/hosts.
- ``revert-create-jail`` needs sanity test for when jail name is invalid.
- ``dhcp_server`` should not assume ``dns_cache`` is running on the LAN. Add optional dependency notice. dns_cache recipe should also warn if ``dhcp_server`` detected on LAN, and how to change ``domain-name-servers``.
- ``upgrade-repo-from-upstream``: check for new scripts fails on subsequent runs on other servers. Fixed by looking for script updates in ``update_local_repo``.
- FDO_LAN_SUBNET_B should be read from /usr/local/etc/fdo/net_iface_lan.conf to make everything dynamic.
- Check why /usr/local/share/pixmaps/FreeBSD-beastie(1440x900).xpm and /usr/home/ are owned by the arbitrary login user.
- fdo-hotdesk-remove-user: terminal output formatting is broken (escape characters).
- setup-vnc-desktop: home folder permissions of arbitrary login user gets clobbered to ownership of root:wheel during create-jail-from-recipe.
- ``update-script``: add sanity test to determine if system script differs from repo script.
- ``add|update-script|config``: use 'cp -p' instead of just 'cp' so that permissions and ownership are carried over.
