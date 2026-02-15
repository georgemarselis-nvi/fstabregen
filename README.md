# fstabgen
Rust CLI that minimally reconstructs /etc/fstab from current mounts. Parses /proc/self/mountinfo, resolves stable identifiers via blkid, filters pseudo and transient filesystems, and emits deterministic entries. NFS and SMB mounts are reconstructed but commented out to keep the result minimal and recovery-safe.
