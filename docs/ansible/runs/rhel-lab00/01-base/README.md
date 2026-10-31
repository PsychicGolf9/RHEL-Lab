# Failed Attempts and TPM Notes

| Run | Failure | Cause |
| --- | ------- | ----- |
| 07:19 | Refuse to alter an already enrolled target | Assert rejected a token that already existed |
| 07:54 | dict2items on a non-dict | Wrong data shape for existing tokens |
| 07:59 | Enroll failed_when tripped | Inverted filter in tpm2_targets_to_enroll array |
| 08:20 | failed_when referenced .results | Loop result handled as list |

## Analysis

The first change was a parsing error with the LUKS JSON metadata resulting in
the PCR check trying to evaluate 7 == "\[7\]" which always returned false. The
fix was to flatten and map the JSON object style array to integers, causing
them to be evaluated properly.

Change two occurred while trying to fix the first and was solved by removing
the dict2items call entirely.

Change number three ended up being the cause for the entire enrollment task to
be bypassed, where the array filter was set to reject the targets that do need
to be enrolled and try to enroll the ones that already have the token. The fix
was a quick flip of rejectattr to selectattr for the array.

The fourth change was an error while diagnosing the third.

## A Note On These Runs

These runs were meant to test the playbooks when a target is already configured
manually, not from a fresh state, especially the TPM tasks. Before promoting
the playbooks 00-bootstrap.yml and 01-base.yml to rhel-lab01, a new node named
rhel-lab02 will be created with a fresh install and the playbooks run again to
catch any errors that may happen during a cold-build.
