# InterGenOS Mirror Transparency Log (DR Backup)

This repository is the append-only transparency log + disaster-recovery backup
for the InterGenOS package mirror at https://repo.intergenos.org/.

## Purpose

`scripts/publish-repo.sh` in `InterGenJLU/intergenos` commits each published
`InterGenOS.db` signed index + per-publish manifest to this repo as an
append-only attestation chain. Operators + auditors can clone this repo to
reconstruct mirror state at any past publish point.

## Layout

    x86_64/
      current/
        InterGenOS.db          # signed index at last publish
        InterGenOS.db.sig      # detached signature
        publish-manifest.json  # per-publish metadata

## DR purpose

If the live mirror at repo.intergenos.org is lost or corrupted, this repo's
HEAD reflects the last verified published state. Restoration: pull the
latest commit, restore packages from independent archive cache, verify
against `InterGenOS.db` checksums.

## Trust anchor

Master signing pubkey fingerprint: `5597A3E0587B253006D0DD7B8C50826182083050`
See `docs/signing-key.md` + `docs/signing-key.asc` in the main
`InterGenJLU/intergenos` repository for the full key + verification chain.

## First publish gating note

This repo was seeded `2026-05-22` to unblock USA-1 audit B12. Real append-only
attestation chain begins with the first run of `publish-repo.sh` end-to-end
(USA-1 B13 closure).
