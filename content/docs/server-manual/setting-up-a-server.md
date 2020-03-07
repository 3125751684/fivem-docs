---
title: 设置服务器
weight: 310
description: >
  设置FXServer的分步指南。
---

运行FXServer
================

FXServer是当前CitizenFX服务器版本的名称。此页面显示了如何运行它。

Having trouble running your server? Visit [server issues][server-issues], use the Discord [#fxserver-support][fxserver-support] channel or create a topic in the [Server Discussion][fxserver-support-category] sub-category on the forum.

Windows
-------

#### Prerequisites
1. [Visual C++ Redistributable 2019][vcredist] or newer.
2. [Git][git-scm] to assure a correct installation.

#### Installation
1. Create a new directory (for example `D:\FXServer\server`), this will be used for the server binaries.
2. Download the latest `master` branch build for Windows from the [artifacts server][windows-artifacts].
3. Extract the build into the directory previously created.
  <br>3b. Use any archiving tool (such as WinRAR or 7-Zip).
4. Clone [cfx-server-data][server-data] in a new folder outside of your server binaries folder, for example, `D:\FXServer\server-data`.
  <br>4b. `git clone https://github.com/citizenfx/cfx-server-data.git server-data`
5. Make a **server.cfg** file in your `server-data` folder (copy the [example server.cfg](#servercfgexample) file below into that file).
6. Generate a license key at <https://keymaster.fivem.net>.
7. Set the license key in your server.cfg using `sv_licenseKey "licenseKeyGoesHere"`.
8. Run the server from the `server-data` folder. For example, in a plain Windows command prompt (cmd.exe) window: 
    ```dos
    cd /d D:\FXServer\server-data
    D:\FXServer\server\run.cmd +exec server.cfg
    ```

    (the `/d` flag is only needed when changing directory to somewhere on a different drive)

---

Linux
-----
1. Create a new folder (for example `mkdir /home/username/FXServer/server`), this will be used for the server binaries.
2. Download the latest `master` branch build for Linux from the [artifacts server][linux-artifacts](copy the URL for the latest server version and use `wget <url>` to download it).
3. Extract the build to the directory that was previously created, using `cd /home/username/FXServer/server && tar xf fx.tar.xz` (you need to have `xz` installed, on Debian/Ubuntu this is in the `xz-utils` package).
4. Clone [cfx-server-data][server-data] in a new folder outside of your server binaries folder.
  <br>4b. For example `git clone https://github.com/citizenfx/cfx-server-data.git /home/username/FXServer/server-data`
5. Make a **server.cfg** file in your `server-data` folder (copy the [example server.cfg](#servercfgexample) file below into that file).
6. Generate a license key at <https://keymaster.fivem.net>.
7. Set the license key in your `server.cfg` using `sv_licenseKey "licenseKeyGoesHere"`.
8. Run the server from the `server-data` folder.
  <br>8b. `bash /home/username/FXServer/server/run.sh +exec server.cfg`

Common issues
---------------

- If you don't get any 'resources found', and it says 'Failed to start resource', you didn't 'cd' to the right folder.
- If you get a lot of errors about citizen:/scripting/, you didn't use run.cmd.
- If nothing happens at all except 'sending heartbeat', you didn't use run.cmd **and** failed to cd to the folder.
- If no resources get started, and you can't connect, you didn't add +exec.
- If you get 'no license key was specified', one of the above things applies.

<a name="servercfgexample"></a>server.cfg
----------

An example server.cfg follows.

```sh
# Only change the IP if you're using a server with multiple network interfaces, otherwise change the port only.
endpoint_add_tcp "0.0.0.0:30120"
endpoint_add_udp "0.0.0.0:30120"

# These resources will start by default.
ensure mapmanager
ensure chat
ensure spawnmanager
ensure sessionmanager
ensure fivem
ensure hardcap
ensure rconlog
ensure scoreboard

# This allows players to use scripthook-based plugins such as the legacy Lambda Menu.
# Set this to 1 to allow scripthook. Do note that this does _not_ guarantee players won't be able to use external plugins.
sv_scriptHookAllowed 0

# Uncomment this and set a password to enable RCON. Make sure to change the password - it should look like rcon_password "YOURPASSWORD"
#rcon_password ""

# A comma-separated list of tags for your server.
# For example:
# - sets tags "drifting, cars, racing"
# Or:
# - sets tags "roleplay, military, tanks"
sets tags "default"

# A valid locale identifier for your server's primary language.
# For example "en-US", "fr-CA", "nl-NL", "de-DE", "en-GB", "pt-BR"
sets locale "root-AQ" 
# please DO replace root-AQ on the line ABOVE with a real language! :)

# Set an optional server info and connecting banner image url.
# Size doesn't matter, any banner sized image will be fine.
#sets banner_detail "https://url.to/image.png"
#sets banner_connecting "https://url.to/image.png"

# Set your server's hostname
sv_hostname "FXServer, but unconfigured"

# Nested configs!
#exec server_internal.cfg

# Loading a server icon (96x96 PNG file)
#load_server_icon myLogo.png

# convars which can be used in scripts
set temp_convar "hey world!"

# Uncomment this line if you do not want your server to be listed in the server browser.
# Do not edit it if you *do* want your server listed.
#sv_master1 ""

# Add system admins
add_ace group.admin command allow # allow all commands
add_ace group.admin command.quit deny # but don't allow quit
add_principal identifier.fivem:1 group.admin # add the admin to the group

# Hide player endpoints in external log output.
sv_endpointprivacy true

# Server player slot limit (must be between 1 and 32, unless using OneSync)
sv_maxclients 32

# Steam Web API key, if you want to use Steam authentication (https://steamcommunity.com/dev/apikey)
# -> replace "" with the key
set steam_webApiKey ""

# License key for your server (https://keymaster.fivem.net)
sv_licenseKey changeme
```

What's next?
------------

- [Using server commands][server-commands]
- [Start scripting][scripting-introduction]

[windows-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_server_windows/master/
[linux-artifacts]: https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/
[server-data]: https://github.com/citizenfx/cfx-server-data

[vcredist]: https://aka.ms/vs/16/release/VC_redist.x64.exe
[winrar]: https://www.rarlab.com/download.htm
[7zip]: https://www.7-zip.org/download.html
[git-scm]: https://git-scm.com/download/win

[server-issues]: /docs/support/server-issues
[server-commands]: /docs/server-manual/server-commands
[scripting-introduction]: /docs/scripting-manual/introduction

[fxserver-support]: https://discord.gg/UwvVgsJ
[fxserver-support-category]: https://forum.fivem.net/c/server-development/server-discussion
