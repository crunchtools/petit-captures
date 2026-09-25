# petit-captures

Every reboot capture taken by [petit](https://github.com/crunchtools/petit)'s
weekly Fingerprints workflow (`tools/fingerprints/refresh.py`).

    <date>/<run>/<release>/   <run> is the petit Actions run ID
      meta.json          image, digest, kernel and OS behind the capture
      a.log, b.log       the reboot event, as petit's corpora use it
      raw/<a|b>/         everything the guest logged on both boots, whole
        previous.log.xz  the boot that rebooted (journald)
        current.log.xz   the boot after it (journald)
        messages.log.xz  /var/log/messages, on releases without journald
        kernel, os-release

Each release is booted from its own cloud image under QEMU/KVM. Addresses,
MACs and IDs are rewritten to documentation ranges (RFC 5737, RFC 3849,
RFC 7042) before anything is written, so nothing here identifies a real
machine.

The 2026-09-25 captures predate `raw/` and hold only the reboot events.
