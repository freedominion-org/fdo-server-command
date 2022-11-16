fdo-server BUGS list:
=====================


BUGS
----

*Currently there are known bugs.*

- ``fdo-dns_cache-add|remove-hostname`` assumes that dns_cache jail is running. It should work even when dns_cache recipe jail is stopped.
- ``fdo-file_server-edit`` assumes that the file_server recipe jail is running. It should work even when the jail is stopped".
- ``fdo-dhcp-edit`` assumes that the dhcp_server recipe jail is running. It should work even when the jail is stopped".


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
- Permissions on install_file_tree for init-vnc-desktop sets arbitrary users home folder to root:wheel.
- ``/etc/hosts`` missing IP address in front of host name.
- ``uclcmd`` can't set string that start with number, e.g: 100GB_Scratch/100GB_Scratch.
- ``create-vm-template|instance``: during eject iso image, it should not say 'as the ISO image to detach' (eject).
- ``create-vm-template|instance``: should be able to cancel and eject iso image. Same with insert, attach, detach.
- ``patch-host``: doesn't seem to update FreeBSD version info.
- ``fdo-server create-vm-instance``: 'template_name' is not being set.
- ``fdo-dns_cache-add-hostname``: hostname validation test won't allow simple hostnames (with no tld), e.g. "blah".
- ``fdo-server create-jail``: error message 'egrep: repetition-operator operand invalid' after "Now we need to check if there are any unsaved changes to this hosts registered config files...". May only happen on FreeBSD 13.1.
- ``dns_cache`` recipe: fails trying to cp /etc/resolv.conf to empty folders in /jls/, check for /jls/jailname/etc/ dir first. If /jls/jailname/etc/resolv.conf does not exist, warn and ask if we want to cp it.
- ``file_server`` recipe: apache22 vhost config needs the RequestHeader fix.
- pf port forward rules for port 22 [ssh] (init-jails) and port 80/443 (http_gateway recipe) should be "any to $host_ip" instead of "any to any".
- ``file_server`` recipe: httpd.conf needs "NameVirtualHost JAIL_IP:80" directive to support multiple VirtualHosts.
- ``fdo-pf-add-port-forward-rule`` generates "fatal: not a git repository (or any of the parent directories): .git" after "Now we need to check ... unsaved changes ..." and before "Would you like to reload the pf ...".
- ``ldap_provider`` recipe: change order of slapd.conf directives to allow sync from consumer to work.
- ``fdo-server create-recipe-jail``: false WARNING about jail named 'ldap' in /etc/rc.conf when there is only 'ldap_consumer' in jail_list.
- ``http_gateway`` recipe: set worker_processes correctly in 'nginx.conf'. It was always '1' because the substitution variable was not used.
- ``init-jails`` and ``create-recipe-jail``: move restart of network services to the end, after everything else is done, and ask user first. Thus not breaking connection used to run the command. 
- ``file_server`` recipe: do not consider ERROR if /dav directory already exists, maybe just set permissions and move on.
- ``init-host``: replace DHCP with SYNCDHCP in /etc/rc.conf.
- ``init-host``: replace '$ext_if' with '$ext_if:0' in nat rule, in order to limit LAN NAT traffic to the primary IP.
- ``fdo-server init-host`` (on static IP primary_local) -> ``fdo-server init-jails`` -> ``fdo-server create-recipe-jail dns_cache``: /etc/resolv.conf should be same as /etc/resolv.conf.static, but it gets clobbered or remains the same as the original from before 'init-host'. Never found the actual cause, decided to disable resolvconf and simplify by always copying /etc/resolv.conf.static to /etc/resolv.conf.
