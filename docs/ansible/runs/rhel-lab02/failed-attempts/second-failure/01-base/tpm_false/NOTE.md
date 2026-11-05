# Failure Hypothesis

Host key verification failed because the node was wasn't manually SSH'd into
first in order to accept the fingerprint.

In addition to the above, the SSH pubkey was written to the node's
authorizedkeys file to avoid another error or lockout during 01-base.
