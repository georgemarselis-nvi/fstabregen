# fstabgen
Rust CLI that minimally reconstructs /etc/fstab from current mounts. Parses /proc/self/mountinfo, resolves stable identifiers via blkid, filters pseudo and transient filesystems, and emits deterministic entries. NFS and SMB mounts are reconstructed but commented out to keep the result minimal and recovery-safe.


Max scope:

* Full `/proc/self/mountinfo` graph reconstruction including bind, move, shared mounts
* LUKS, LVM, MD RAID, Btrfs subvol/raid, ZFS dataset inference
* Accurate option canonicalization per FS type
* Network FS auth redaction + templating
* systemd unit generation parity
* Cross-distro heuristics + validation mode
* Idempotent diff against existing fstab

--check/--diff modes

<!-- Yes - if it can emit deterministic output and nonzero exit on ambiguity, Ansible can run it (command module) then copy/template the generated file, optionally gated by --check/--diff modes.
Key requirement is stable, machine-parseable output (JSON and/or plain fstab) plus idempotency controls.

mount topology auditor"

A tool that models the full live mount graph - not just static fstab entries.

It parses /proc/self/mountinfo, builds parent-child and bind relationships, detects propagation, shared trees, overlay stacks, device ancestry (LUKS->LVM->FS), and validates consistency against policy or fstab.

It audits structure, invariants, and drift - not just regenerating lines.

Utility:

* Detect configuration drift between live mounts and policy
* Verify invariants: no rw on sensitive paths, no unexpected bind/propagation
* Validate storage stacks LUKS→LVM→FS correctness
* Audit network mounts and exposure surface
* Pre-flight checks before backup, chroot, or container runtime start

It becomes a compliance and integrity verifier.
does such a "mount topology auditor" exist?

Not as a single cohesive tool.

Closest components:

findmnt - topology view and JSON export

systemd-analyze verify - unit validation

lsblk - device stack graph

Compliance tools like OpenSCAP - policy checks

No dedicated mount graph auditor with full stack + invariant engine is common.

-->
