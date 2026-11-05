# Note On These Docs

**The runs for rhel-lab02 are meant to display a clean cold-build output. Any run
that failed was placed in the failed-attempts folder with notes on what failed.**

## Cold-Build

### Process Summary

- Boot Rocky/RHEL ISO as VM or on bare metal.
- Take specific note of WLAN interface name when setting hostname. This is
  the only mandatory variable that can't be found afterwards without SSH.
- Defaults for everything, except:
  - Select "Encrypt My System" or whatever to enable LUKS. If you want TPM,
    You must do that now, because it's a pain later.
  - Choose minimal install... Unless you really want a GUI for a headless
    system.
- Make sure to lock the root account
- Whatever username you type in, make sure it's in your group_vars for
  later. Make them an administrator by hitting the toggle and set a
  password that you don't mind entering a bunch of times and will remember.
- Fill out the bash_inventory found in scripts/
- Run the scripts/ directory in this order:
  1. wg_setup.sh
  2. luks_passphrase.sh
  3. ansible_run_log.sh

**Important:** Make sure you do the ssh-key process described below before
           running the playbooks. Not having your admin keys enrolled on the
           node will result in a lockout.

**Note:** You don't have to us the ansible_run_log.sh script, it's just a good
      thing to have for the docs.

### SSH Key Enrollment

Make sure you run ssh-keygen for the ansible user. You can reuse your SSH keys
for your admin user, but you must have at least one.

You MUST ssh-copy-id or scp your human user keys to the node. You'll get locked
out later if you don't and need to access the node through the console to fix
it. I said this twice for a reason.

You need to add the \[Peer\] section in your control machine's WireGuard
config.

Make note of the location for the ansible user's public key and put it in
host_vars.

Also make sure you ssh in manually at least once to confirm the fingerprint.

As much of this as possible will be automated in the future.
