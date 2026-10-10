# petit-captures Constitution

> **Version:** 1.0.0
> **Ratified:** 2026-10-02
> **Status:** Active
> **Inherits:** [crunchtools/constitution](https://github.com/crunchtools/constitution) v1.22.0
> **Profile:** Data Archive

This file holds what is specific to petit-captures. The fleet rules and the
Data Archive profile apply at the inherited version and are checked against
this repo's files by `constitution.yml`. They are not restated here.

## Producer and Scrubbing

- **Producer:** the `archive` job of `.github/workflows/fingerprints.yml` in
  [crunchtools/petit](https://github.com/crunchtools/petit), weekly and on
  demand. It pushes one commit per run straight to the default branch with
  the `CRUNCHTOOLS_DISPATCH_TOKEN` secret; nothing else writes here.
- **Key:** `<date>/<run>/<release>/`, where `<run>` is the petit Actions run
  ID, so a second run on the same day adds a directory instead of
  overwriting one. The layout is described in the README.
- **Scrubbing:** `scrub()` in petit's `tools/fingerprints/refresh.py`
  rewrites IPv4 addresses to `192.0.2.0/24` (RFC 5737), IPv6 to
  `2001:db8::/32` (RFC 3849) and MACs to `00:00:5e:00:53:xx` (RFC 7042),
  one stand-in per value across both boots, and zeroes UUIDs and 32-hex IDs.
  `assert_clean()` then refuses to write a capture that still carries the
  runner's hostname, user or a non-documentation IPv4 address.
- **Source:** every capture is a guest booted from a distribution's own
  cloud image under QEMU/KVM on a GitHub runner, never a real machine.
  Raw logs are xz-compressed; the 2026-09-25 captures predate `raw/` and
  hold only the reboot events.

## History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-10-02 | Initial manifest under constitution v1.18.0 |
