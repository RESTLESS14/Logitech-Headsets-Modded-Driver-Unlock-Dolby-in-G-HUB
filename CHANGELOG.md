# v1.1.0 — G HUB cache update

G HUB can create a replacement cache after the cache file is renamed. The updated procedure patches the active cache package in place and retains the filename G HUB expects.

`Patch-GHubCache.ps1` reads `%ProgramData%\LGHUB\current.json`, backs up the active package, updates the Dolby device definitions in `devices_0001.json` and `devices_0002.json`, and verifies the result. It does not modify `current.json`. Do not rename the cache file manually.

Full setup includes driver cleanup and installation, Dolby files, the cache patch, and a backed-up reset of `settings.db`. Dolby unlock only applies the Dolby files and cache patch without reinstalling the driver or resetting settings.

The setup package (`SETUP.bat` and its complete `Payload` folder) is distributed separately and is not attached to this release. v1.1.0 does not include a new audio-driver build. The original v1.0.0 package remains available as the previous release.