# sh-apple — self-hosted apple node

iMac running debian node for backing up my self-hosted data by rsync.

## Hardware

- External HDD for backups on `/mnt/backup`

## Running:

```bash
git clone --recurse-submodules git@github.com:tikhonp/sh-apple.git
cd sh-apple
docker compose up -d
```

## Backup target

Blackberry pushes its backup mirror here nightly (05:00, `backup-to-remote-server` →
`rsync-server` over the tailnet). `/mnt/backup` stays a plain browsable mirror, guarded:

- `/mnt/backup/.backup-canary` — proves the disk is mounted; the sync **refuses to run**
  if it's missing. One-time setup after mounting a (new) backup disk:

  ```bash
  touch /mnt/backup/.backup-canary
  ```

- `/mnt/backup/.trash/<date>/` — files deleted or overwritten by a sync are moved here
  instead of destroyed, and pruned after ~30 days (sync and prune are both driven from
  blackberry over ssh). To restore something, copy it back from the dated folder into
  the mirror.

# License

Tikhon Petrishchev 2025. All rights reserved.
