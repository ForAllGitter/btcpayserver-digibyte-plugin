# DigiByte Chain Snapshots

## Why Snapshots Matter

A full DigiByte node can take a long time to sync from genesis. Snapshots allow operators to bootstrap much faster.

---

## Recommended Snapshot Process

1. Stop DigiByte Core cleanly.
2. Create a compressed archive of the `blocks` and `chainstate` directories.
3. Record the block height and hash at the time of the snapshot.
4. Publish the snapshot with a checksum (SHA256).

---

## Verification Steps

After downloading a snapshot:

```bash
# 1. Verify checksum
sha256sum -c snapshot.sha256

# 2. Extract into the DigiByte data directory
# 3. Start DigiByte Core
# 4. Confirm it continues syncing from the snapshot height
```

---

## Trust Trade-offs

Using a third-party snapshot means you are temporarily trusting the snapshot provider. Always:

- Prefer snapshots from well-known community sources
- Verify the final chain tip against multiple explorers after sync
- Consider reindexing (`-reindex`) if you need maximum confidence

This document should be updated whenever the community snapshot process changes.
