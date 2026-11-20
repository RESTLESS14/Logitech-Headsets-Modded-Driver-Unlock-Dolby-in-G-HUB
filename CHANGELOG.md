# Project Updates

## v1.1.0 — G HUB cache handling update

### Why this update

Logitech G HUB changed how it locates and rebuilds its device cache. The previous manual instructions asked users to rename the largest cache file; that method can make G HUB create a fresh cache and ignore the modified device definitions.

### Updated cache method

- Identify the active core-cache package through `%ProgramData%\LGHUB\current.json`.
- Patch the active package in place and keep its original hash-based filename.
- Update only the Dolby device-definition entries in the cache.
- Back up the original cache before applying changes and verify the patched entries.
- Do not rename the cache file manually.

### Setup notes

- The setup package is distributed separately from this repository. Keep `SETUP.bat` together with its complete `Payload` folder.
- Use the updated setup package's **Full setup** or **Dolby unlock only** option as appropriate.
- This is a cache-handling and installation-guide update. It does not introduce a new audio-driver build, and this release does not include the separately distributed setup package.

### Preserved documentation

The original `README.md` remains unchanged and retains the previous guide. This update is documented separately so users can distinguish the original instructions from the newer cache workflow.