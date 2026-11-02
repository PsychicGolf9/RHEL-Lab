# Failure Note

## First Failure

Returned an error that `systemd-cryptenroll` found no usable TPM2 device. This is
because the emulated TPM2 device was never enabled via KVM. The role caught
that correctly. The device will be enabled, VM rebooted, and the playbook run
again.

## Second Failure

Returned an error in `roles/tpm2/tasks/enroll.yml` that was hidden by having
no_log set to `true`. The error deduced to be the `--unlock-key-file=-` line by
examining the logs for `tpm2_targets_to_enroll` success in previous tasks,
matching the LUKS passphrase with the vaulted variable, and ensuring that the
`tpm2_pcrs` variable was set in the `defaults/main.yml` for the role.

### Finding the Right Option

The node was SSH'd into over the WireGuard tunnel and the following commands
were attempted manually with a prompted passphrase with `read -rs` and piped
to the following `systemd-cryptenroll` options:

  1. `--unlock-key-file=-`
    - Returned: `unrecognized option`
  2. `--unlock-key-file=/dev/stdin`
    - Returned: `unrecognized option`
  3. Setting `env PASSWORD="$PW"` and removing `--unlock-key-file` altogether
    - Returned `New TPM2 token enrolled as key slot 1`
    - This verified the suspicion that `--unlock-key-file=-` was invalid.

The `roles/tpm2/tasks/enroll.yml` task will be updated in the next commit to reflect
this bug fix. The slot will be wiped from the node's keyslots in order to test
again.
