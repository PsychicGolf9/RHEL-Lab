# Run Note

This playbook was run once with tpm2_enabled set to false first, and then again
with it set to true to test the opt-in and tpm2 role separately. Find both sets
of logs in their respective directories. The tp2 logs will show changed=0 due
to this fact.

It was tested by using SSH over the tunnel via both admin and ansible users
prior to the tpm2_enabled: true run.
