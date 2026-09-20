A guide on how to **download** and **install mods** in [Valheim](https://store.steampowered.com/app/892970/Valheim/) on PC, covering mod managers and manual installation on Windows, Linux and macOS.

Valheim runs on Unity and its mods are [BepInEx](https://github.com/BepInEx/BepInEx) plugins. The community maintains its own BepInEx build rather than using the upstream one, and that is the first thing to get right.

Our example is [EpicLoot](https://thunderstore.io/c/valheim/p/RandyKnapp/EpicLoot/), a long-running loot and magic item overhaul. It is a good demonstration case because it pulls in real dependencies and because it has to be installed on the server as well as the client.

[**View Guide On TMC (Recommended Due To Better Formatting)**](https://moddingcommunity.com/blog/how-to-install-mods-in-valheim/)

## Table Of Contents
* [Requirements](#requirements)
* [Which Version Of Valheim You Own Matters](#which-version-of-valheim-you-own-matters)
* [BepInExPack Valheim](#bepinexpack-valheim)
* [Installing With A Thunderstore Mod Manager](#installing-with-a-thunderstore-mod-manager)
* [Installing With Vortex](#installing-with-vortex)
* [Installing Manually](#installing-manually)
    * [Windows](#windows)
    * [Linux](#linux)
    * [macOS](#macos)
* [Installing With The TMC App](#installing-with-the-tmc-app)
* [Server-Side Mods And Multiplayer](#server-side-mods-and-multiplayer)
* [Configuring Mods](#configuring-mods)
* [Checking Everything Loaded](#checking-everything-loaded)
* [Updating And Uninstalling](#updating-and-uninstalling)
* [Troubleshooting](#troubleshooting)
* [Conclusion](#conclusion)
* [See Also](#see-also)

## Requirements
* A PC running **Windows 10** or later, **Linux**, or **macOS**. Valheim has native builds for all three.
* **Valheim**, ideally the **Steam** version. See the next section for why.
* A few hundred MB free. Big overhauls like EpicLoot are larger.
* [7-Zip](https://www.7-zip.org/) or any archive tool if you install by hand.
* A backup of your worlds and characters before you start. They live in `%userprofile%\AppData\LocalLow\IronGate\Valheim` on Windows.

**WARNING** - Take that backup seriously. Mods that add items and progression, EpicLoot included, write data into your save. Removing such a mod later can leave you with a character holding items the game no longer recognises.

## Which Version Of Valheim You Own Matters
Valheim is sold on Steam, on the Microsoft Store, and on Xbox consoles.

* **Steam** is the version everything in this guide assumes, and the version the whole mod scene targets.
* **Microsoft Store and Game Pass** installs live under `C:\XboxGames\Valheim\Content` and are far harder to mod. BepInEx has to write files into the game folder, and these installs are protected in ways that generally get in the way. There is no supported path here and you should not expect mod managers to work.
* **Xbox consoles** cannot be modded at all. Crossplay lets an Xbox player join a PC server, but the Xbox client is still vanilla and cannot load anything.

## BepInExPack Valheim
[BepInExPack Valheim](https://thunderstore.io/c/valheim/p/denikson/BepInExPack_Valheim/) is the loader, and it is not plain BepInEx. It is a Valheim-specific build maintained by Azumatt, Vapok and Margmas, with a preconfigured `BepInEx.cfg`, launch scripts for Linux and the dedicated server, preloader changes several mods depend on, and semantic version support that upstream BepInEx 5 throws out.

Install that pack, not generic BepInEx.

**NOTE** - Because it is a community fork, the official BepInEx Discord cannot help you with Valheim problems, and they will tell you as much. Take Valheim issues to the Valheim modding community instead.

On top of BepInEx, EpicLoot depends on two shared libraries:

* **[Jötunn](https://thunderstore.io/c/valheim/p/ValheimModding/Jotunn/)**, the Valheim modding library that most substantial mods build against.
* **JsonDotNET**, a packaged copy of Newtonsoft.Json.

Mod managers install both automatically.

## Installing With A Thunderstore Mod Manager
This is the most travelled path and the one mod pages link to.

Three managers work with Valheim and all three read the same profile format:

| Manager | Platforms |
| ------- | --------- |
| [Gale](https://thunderstore.io/c/valheim/p/Kesomannen/GaleModManager/) | Windows, Linux |
| [Thunderstore Mod Manager](https://www.overwolf.com/app/Thunderstore-Thunderstore_Mod_Manager) | Windows |
| [r2modman](https://thunderstore.io/c/valheim/p/ebkr/r2modman/) | Windows, Linux, macOS |

The steps are the same whichever you pick:

1. Install the manager and select **Valheim**.
2. Create a profile.
3. Browse or search for **EpicLoot**.
4. Click **Install** or **Download with dependencies**. BepInExPack Valheim, Jötunn and JsonDotNET come along with it.
5. Launch the game through the manager with **Start modded** or **Launch game (modded)**.

Launching Valheim from Steam directly runs it vanilla, since the manager attaches BepInEx at launch time.

## Installing With Vortex
[Vortex](https://www.nexusmods.com/about/vortex/) supports Valheim and pulls from [Nexus Mods](https://www.nexusmods.com/valheim) rather than Thunderstore. The Nexus Valheim catalogue is much smaller and most authors publish to Thunderstore first, so use this if Vortex is already your tool of choice and you have found what you want there.

1. Install Vortex and sign in.
2. Under **Games**, search for **Valheim**, hover the tile and click **Manage**.
3. Install BepInExPack Valheim yourself using the manual steps below. Vortex will not set the loader up for you.
4. Download mods from Nexus with **Mod Manager Download**, then **Install** and **Enable**.
5. Launch from Steam as normal. Vortex writes files into the game folder permanently, so no special launch is needed once BepInEx is in place.

**WARNING** - Do not run Vortex and a Thunderstore manager against the same install. They both want to own `BepInEx/plugins` and will undo each other's work.

## Installing Manually
First, find your game folder. Right-click **Valheim** in Steam, then **Manage** and **Browse local files**:

```
C:\Program Files (x86)\Steam\steamapps\common\Valheim
```

Download [BepInExPack Valheim](https://thunderstore.io/c/valheim/p/denikson/BepInExPack_Valheim/) with **Manual Download**, extract it somewhere that is **not** the game folder, then move the contents of the `BepInExPack_Valheim` folder into your Valheim folder. Done right, you will see `BepInEx`, `winhttp.dll` and `doorstop_config.ini` sitting next to `valheim.exe`.

Then download EpicLoot, Jötunn and JsonDotNET, extract each, and copy their `.dll` files into `Valheim\BepInEx\plugins`.

What you do next depends on your platform.

### Windows
Nothing else to do. Launch the game and a BepInEx console window should appear alongside it.

### Linux
1. Make the launch script executable:

```bash
chmod u+x start_game_bepinex.sh
```

2. In Steam, open Valheim's **Properties** and set the launch options to:

```
./start_game_bepinex.sh %command%
```

3. Launch through Steam.

You can also give the full path to the script instead of a relative one, which lets you keep the pack outside the game folder entirely.

### macOS
Valheim has a native macOS build, but BepInEx 5 does not run natively on Apple Silicon, because it depends on MonoMod and MonoMod has no arm64 support yet. The workaround is to force the game through Rosetta.

1. Make the script executable:

```bash
chmod u+x start_game_bepinex.sh
```

2. Set Valheim's Steam launch options to:

```
/usr/bin/arch -x86_64 /bin/bash ./start_game_bepinex.sh %command%
```

3. Launch through Steam.

Leave off the `arch -x86_64` part on an M-series Mac and the game still starts, it just starts without BepInEx and loads none of your mods. Intel Macs do not need it.

## Installing With The TMC App
Valheim is one of the games [the TMC App](https://moddingcommunity.com/tmc-app) already supports, so unlike most of our guides this is a real option rather than a promise. The app is our own mod manager and server browser, and it deploys Valheim mods into `BepInEx/plugins` like everything else here.

Installing it:

* **Linux**: one line, no root and no package manager.

```bash
curl -fsSL https://raw.githubusercontent.com/modcommunity/tmc-app/main/scripts/install.sh | sh
```

* **Windows**: the `setup.exe` or `setup.msi` from the [releases page](https://github.com/modcommunity/tmc-app/releases). There is a portable build too, though it does not register the launcher entry or the `tmc://` link handler.
* **macOS**: the `.dmg` from the same releases page.

Once it is installed:

1. Open the app and add **Valheim**, pointing it at your Steam install folder.
2. Create a **sandbox**. Sandboxes are named mod profiles with their own load order and deployment method, and switching between them does not re-download anything.
3. Install the mods you want into that sandbox.
4. Launch the game.

**WARNING** - Please read this part before you rely on it. **The app is in very early development** and we would rather say so than have you find out mid-playthrough. Its own README lists every supported game as untested, Valheim included, so treat it as something to experiment with alongside Gale or r2modman rather than as a replacement for them. Keep the backup we mentioned in the requirements.

That said, this is exactly the stage where trying it is most useful. If it works, we would like to know. If it deploys into the wrong folder or mangles your load order, we would **really** like to know, and that kind of report is worth more to the project right now than almost anything else.

The app is **open source** under GPL-3.0 at [github.com/modcommunity/tmc-app](https://github.com/modcommunity/tmc-app). Bug reports and feature requests go in [the issue tracker](https://github.com/modcommunity/tmc-app/issues), pull requests are welcome, and the repository documents how per-game rules work if you want to improve the Valheim side yourself.

## Server-Side Mods And Multiplayer
This is the part that catches Valheim players out, because it works differently from most co-op games.

Valheim mods split roughly three ways:

* **Client only.** UI tweaks, camera changes, visual mods. Install on your machine and nothing else cares.
* **Client and server.** Anything that adds items, recipes, creatures or progression. EpicLoot is squarely here, and it has to be installed on the dedicated server as well as on every player's client.
* **Server only.** Admin tooling, backups, world management.

Getting this wrong usually shows up as being kicked on connect with a version mismatch, or as items vanishing because the server does not know what they are.

For a dedicated server, BepInExPack Valheim ships a `start_server_bepinex.sh` script for exactly this. Make it executable with `chmod u+x start_server_bepinex.sh`, edit its launch parameters the same way you would edit Valheim's own server script, and run it instead of `start_server.sh`.

If you are setting a server up from scratch, our separate [Valheim server guide](https://moddingcommunity.com/blog/how-to-setup-a-valheim-server/) covers that side.

**TIP** - Several managed Valheim hosts will install BepInEx for you with a toggle. If you would rather not touch a shell, that is a legitimate shortcut.

## Configuring Mods
Mods write their config files here on first run:

```
Valheim\BepInEx\config
```

They are plain text `.cfg` files. EpicLoot puts a lot of its tuning in there, along with JSON files for loot tables and magic effects, and it is well worth a look if you want to adjust rather than accept the defaults.

[BepInEx Configuration Manager](https://thunderstore.io/c/valheim/p/Azumatt/Official_BepInEx_ConfigurationManager/) adds an in-game settings window that edits the same values without alt-tabbing. Gale and r2modman both include config editors too.

## Checking Everything Loaded
On Windows, BepInEx opens a console window next to the game. It appears in the taskbar and you can watch the boot sequence in it.

What you want to see is grey and white text, which is informational output. Colours mean trouble:

| Colour | Meaning |
| ------ | ------- |
| Red | Fatal error |
| Dark red | Error |
| Yellow | Warning |
| Dark grey | Debug output |

The pack also prints its own Thunderstore version to the console, which is separate from the BepInEx version underneath.

For EpicLoot specifically, load a world and check your inventory for the magic item tabs and the augmenting station recipes.

## Updating And Uninstalling
Mod managers flag outdated mods and update them in a click. Do your updating between play sessions rather than mid-playthrough, since a mod that writes to your save can behave badly when versions shift under it.

To remove a mod, uninstall it in your manager or delete its `.dll` from `BepInEx/plugins`. To return to vanilla, delete `BepInEx`, `winhttp.dll`, `doorstop_config.ini` and the launch scripts from the game folder. Steam's file verification will not remove them, because Steam did not install them.

**WARNING** - Before removing a mod that added items to your world, consider whether you want that character and world afterwards. This is what the backup is for.

## Troubleshooting
**No BepInEx console and no mods.** On Windows, check that `winhttp.dll` sits directly beside `valheim.exe`. On Linux, check your launch options include `./start_game_bepinex.sh %command%`. On macOS, check the `arch -x86_64` prefix is there.

**Kicked from a server with a version mismatch.** Your mods and the server's mods do not match. Install the same versions the server runs, or ask the host to export their list.

**Mods stopped working after a Valheim update.** Expected. Iron Gate patches break BepInEx mods and authors need time. Check your mods' Thunderstore pages for updated releases.

**Game crashes at startup.** Move everything out of `BepInEx/plugins`, confirm a clean start, then add mods back in halves to find the offender.

**Mods work in single player but not on my own server.** Server-side mods need to be installed on the server too, not just in the client that hosts it. Use `start_server_bepinex.sh`.

**Microsoft Store version will not mod.** It largely will not, and there is no supported way around it. The Steam version is the one to use.

**Nothing loads on an M-series Mac.** You are missing the Rosetta prefix in your launch options.

## Conclusion
The short version for most people: install Gale or r2modman, pick Valheim, install EpicLoot with dependencies, and launch modded. BepInExPack Valheim comes along and you never have to think about it.

The two Valheim-specific things worth remembering are that the BepInEx pack is a community fork with its own quirks and its own support channels, and that anything touching items or progression has to be installed on the server as well as the client.

Valheim is one of the few games our own [TMC App](https://github.com/modcommunity/tmc-app) already supports. It is open source and very early in development, so it is worth a try rather than worth relying on, and feedback on it would be genuinely appreciated.

## See Also
* [Valheim on Thunderstore](https://thunderstore.io/c/valheim/)
* [Valheim on Nexus Mods](https://www.nexusmods.com/valheim)
* [Valheim Modding Discord](https://discord.gg/RBq2mzeu4z)
* [Valheim Modding Wiki](https://github.com/Valheim-Modding/Wiki/wiki)
* [Official Valheim Modding FAQ](https://valheim.com/support/modding-faq-for-the-asset-bundle-update-0-217-40) - Iron Gate's own notes on the asset bundle system mods have to work with.
* [Jötunn documentation](https://valheim-modding.github.io/Jotunn/)
* [TMC App](https://github.com/modcommunity/tmc-app)

We keep this guide as up-to-date as we can, but Valheim, BepInEx and the mod libraries all update separately. If an instruction here no longer matches what you are seeing, please report it or open a [pull request](https://github.com/modcommunity/how-to-install-mods-in-valheim/pulls) on this guide's GitHub repository.

Join our [Discord server](https://discord.moddingcommunity.com) if you have any questions or want help with anything modding related!
