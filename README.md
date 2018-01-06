# snapper-refresh-qgroup

`snapper-refresh-qgroup` is a script to add snapshots from a snapper config to
the qgroup specified by the `QGROUP` configuration variable. If called with no
command line arguments, it will attempt to do so for all snapper configs shown
by `snapper list-configs` - otherwise, command line arguments are interpreted
as the names of snapper configs on which to operate.

After disabling quotas for a filesystem and then enabling them again, snapper
will resume adding new snapshots to the qgroup specified by the `QGROUP`
configuration variable, if it is recreated. However, existing snapshots will
not be added to the recreated qgroup, and must be added manually, or by using
this script.

This script is intended to work with any POSIX-compliant shell, and is used by
the author with dash as `/bin/sh`. However, it must be run as root, since root
privileges are required for qgroup assignments. It assumes that snapper config
files can be found in the standard `/etc/snapper/configs` directory; if they
are located elsewhere, the `SNAPPER_CONFIG_DIR` environment variable can be set
to the correct directory, or the `DEFAULT_CONFIG_DIR` readonly variable set at
the top of the script can be modified.
