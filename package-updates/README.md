Cloned from https://github.com/pschmitt/zabbix-template-package-updates

# Installation

## Agent setup

### Docker

1. sudo

This template requires `sudo` to be available inside the zabbix-agent container.

You can bind-mount the supplied sudoers config with:
- `-v ./sudoers/alias-chroot.docker:/etc/sudoers.d/alias-chroot:ro`.
- `-v ./sudoers/reboot-required.docker:/etc/sudoers.d/reboot-required:ro`.

Bear in mind that this file should be owned by root and its permissions set to `0600`.

2. You obviously also need to make the script available as well: `-v ./zbx-pkg.sh:/zabbix/bin/zbx-pkg.sh`.

3. Pass the UserParameter config like so: `-v ./zabbix_agentd.d/pkg-updates.docker.conf:/etc/zabbix_agentd.d/pkg-updates.conf:ro`.

4. To be able to chroot inside the host you need mount the rootfs like so: `-v /:/rootfs:ro`.

### OpenWRT

1. You need to install `sudo`:

```
opkg update && opkg install sudo
```

2. Copy `sudoers.d/package-updates.openwrt` to `/etc/sudoers.d/package-updates`.

3. Copy `zbx-pkg.sh` to `/etc/zabbix_zabbix_agentd.d/bin/zbx-pkg.sh`.

4. Copy `zabbix_agentd.d/reboot-required.openwrt.conf` to `/etc/zabbix_zabbix_agentd.d/reboot-required.conf`.

5. Restart the agent: `/etc/init.d/zabbix_agentd restart`.

## Zabbix Server setup

1. Import the template `zabbix_template_package_updates.xml`.

2. Apply it to your hosts
