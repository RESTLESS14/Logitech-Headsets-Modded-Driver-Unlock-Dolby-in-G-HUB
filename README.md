<h1 align="center">🎧 Logitech G HUB Dolby Unlock</h1>

<p align="center"><strong>Community modification for supported Logitech headsets</strong></p>

<p align="center">
  <a href="https://www.techpowerup.com/forums/threads/logitech-headsets-modded-driver-%E2%80%94-unlock-dolby-in-g-hub.352645/">Original TechPowerUp thread</a>
  · Previous guide preserved in <a href="README-OLD.md">README-OLD.md</a>
</p>

> **Current instructions:** This README describes the updated setup workflow. The previous manual guide is kept in [`README-OLD.md`](README-OLD.md) for reference; its cache-renaming step is obsolete. Do not follow that step.

## Contents

- [What this project does](#what-this-project-does)
- [Setup package](#setup-package)
- [Setup options](#setup-options)
- [What the cache patch changes](#what-the-cache-patch-changes)
- [Backups and settings](#backups-and-settings)
- [Before you start](#before-you-start)
- [Compatibility](#compatibility)

## What this project does

This community modification enables Dolby device definitions in Logitech G HUB for supported Logitech headsets. It uses Logitech headset audio-driver files with modifications. It is not affiliated with or endorsed by Logitech.

- Adds Dolby device definitions to G HUB.
- Includes an installer workflow for cleaning up and staging the supplied Logitech audio driver.
- Patches the active G HUB core cache while keeping the filename G HUB expects.
- Includes updated Blue VO!CE 2.0 Effect files for devices that support them.

<p align="center">
  <table>
    <tr>
      <td align="center" width="400">
        <img src="img/DOLBY.png" alt="Dolby in G HUB" width="380"><br>
        <sub>Dolby in G HUB</sub>
      </td>
      <td align="center" width="400">
        <img src="img/Blue%20VO!CE%202.0%20Effect.png" alt="Blue VO!CE 2.0 Effect" width="380"><br>
        <sub>Blue VO!CE 2.0 Effect</sub>
      </td>
    </tr>
  </table>
</p>

## Setup package

The setup package (`SETUP.bat` and its complete `Payload` folder) is distributed separately from this source repository. Keep `SETUP.bat` beside `Payload` after extracting the package, then run `SETUP.bat` as administrator.

## Setup options

### 1. Full setup

The full setup runs these stages in order:

1. **Prepare Windows Audio and G HUB** — stops the relevant audio and G HUB processes/services.
2. **Clean up Logitech audio devices** — removes the selected old Logitech audio-driver packages and ghost devices.
3. **Stage and apply the supplied driver** — stages the package and uses DevCon to apply it to supported connected hardware.
4. **Apply Dolby files** — backs up and updates the device-definition files in the installed G HUB depot, then patches the active core cache.
5. **Reset G HUB settings** — backs up `%LocalAppData%\LGHUB\settings.db`, then removes it so G HUB can rebuild its settings.
6. **Restore services and launch G HUB** — starts Windows Audio and G HUB again.

### 2. Dolby unlock only

This option stops G HUB, backs up and reapplies the Dolby depot files, patches the active core cache, then starts G HUB. It does not reinstall the audio driver or reset `settings.db`.

## What the cache patch changes

`Patch-GHubCache.ps1` reads `%ProgramData%\LGHUB\current.json` to find the active core-cache package. It checks that the package is the largest hash-named cache file, backs up the original, and updates only these entries inside it:

- `data/devices/devices_0001.json`
- `data/devices/devices_0002.json`

The patch verifies the updated entries and preserves the cache filename G HUB expects. **Do not rename the cache file manually.** If the Dolby definitions are already present, the patcher reports that and leaves the cache unchanged.

## Backups and settings

Setup creates timestamped runtime backups under:

```text
%ProgramData%\Logitech-Dolby-Unlock\Backups\<timestamp>
```

Depending on the option and changes made, backups can include the original depot JSON files, the original cache package, and `settings.db`. The setup package may also include static backup-device files under `Payload\DOLBY UNLOCKED FILES\BACKUP DEVICES`; those are package files, separate from the runtime backups captured from your PC.

Resetting `settings.db` can reset local G HUB settings and profile assignments. Back up profiles first:

1. In G HUB, open **Manage Profiles**.
2. Select a profile and open its three-dot menu.
3. Choose **Share** to save it to your Logitech account, or **Backup** to save it locally.

After the reset, you may need to scan for your games again. If a restored profile appears under **Desktop**, use its three-dot menu to copy it to the correct game.

## Before you start

- The full setup adds the third-party `Restless14` certificate to the Windows **Root** and **TrustedPublisher** certificate stores.
- Back up your G HUB profiles before choosing Full setup.
- Disable G HUB automatic updates while using the modification. An update may replace modified depot or cache content. In G HUB, open **Settings → Updates** and turn off **Enable Automatic Updates**.

<p align="center">
  <img src="img/disable-automatic-updates.png" alt="Disable G HUB automatic updates" width="800">
</p>

## Compatibility

| Category | Details |
|---|---|
| Headsets | Logitech G430, G431, G432, G433, G533, G633, G635, G733, G933, G935, PRO X, PRO X Wireless |
| Windows | Windows 10 / Windows 11 |
| G HUB | The setup detects the installed depot; compatibility may vary by G HUB version and headset model. |

Thanks to [Tunnah](https://www.techpowerup.com/forums/members/tunnah.100852/) for feedback on the original TechPowerUp thread.

---

<p align="center"><sub>Community driver modification. Not affiliated with or endorsed by Logitech.</sub></p>