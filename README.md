# PixelPlanetBot
Bot for [pixelplanet.fun](https://pixelplanet.fun).

Original idea was based on [woyken/pixelplanet.fun-bot](https://github.com/Woyken/pixelplanet.fun-bot/).

Now only main (Earth) canvas is supported in all applications, moon canvas will be supported in Watcher/Visualizer, 3D canvas bot support theoretically can be implemented in future.

You can download executable files [here](https://github.com/Topinambur223606/PixelPlanetTools/releases/latest).

### Some important stuff
- PixelPlanet recognizes user by IP, so launching multiple bots on same computer \/ from computers in same LAN would not work.
- Admins allow bots only if they do not bother anyone and if it is not about super huge art in the center of active map segment.
- Dithering or something similar is not provided in bot, color is picked as closest available; use [PixelPlanet converter](https://pixelplanet.fun/convert) or Photoshop "to web" export to get image for building.
- To build EXE with third party DLLs included by yourself, copy [ILRepack utility](https://www.nuget.org/packages/ILRepack/) to `executable` directory, launch "release" profile compilation and combined EXE will appear in that folder.
- After mass attack of russian griefers with proxies in 2019, May captcha was introduced at site, so you should deal with it for bot. When bot asks to pass captcha, you should just open site as usual, place pixel anywhere and then press any key in bot shell window.
- Moon canvas support will not be implemented in bot. That canvas is created for veteran users who build with their hands a lot, so it is supposed to be a bot-free area.

# Usage:
## For all apps:
- Param order is not important;
- By default logs are saved to `%appdata%/PixelPlanetTools/logs/<app name>`;
- Log files are deleted from `%appdata%/PixelPlanetTools/logs` folder and all subfolders (recursively) if older than one week;
- To specify path to your own log file, use `--logFilePath` (if log file exists, new lines are appended);
- To display debug logs in console (a lot of useless info), specify `--showDebug` parameter;
- To disable updates, specify `--disableUpdates` parameter;
- To check for updates manually, specify `--checkUpdates` parameter;
- To get help screen, launch it with `--help` parameter;
- To get app version, launch it with `--version` parameter.

## PixelPlanetBot
Program that builds picture (surprisingly).

### Usage:
- `-x, --leftX` - **required**, X coordinate of left picture pixel;
- `-y, --topY` - **required**, Y coordinate of top picture pixel;
- `-i, --imagePath` - **required**, URI (URL or path) of image that is built;
- `-d, --defenseMode` - makes bot stay opened when picture is finished to provide picture integrity, disabled by default;
- `--notificationMode` - defines bot behaviour when captcha appears, possible values: `sound` (default value), `browser`, `both`;
- `--placingOrder` - determines pixels priority for bot, possible values: `random` (default value), `left`, `right`, `top`, `bottom`, `outline`;
- `--proxyAddress` - proxy that is used by bot, address includes port, empty by default;
- `--proxyUsername` - username for connecting to proxy, empty by default, no proxy authorization if not specified;
- `--proxyPassword` - password for connecting to proxy, empty by default;
- `--useMirror` - if specified, changes base address to [fuckyouarkeros.fun](https://fuckyouarkeros.fun) (site mirror);
- `--serverUrl` - if specified, changes base address to your custom one - for those who deployed their own PixelPlanet copy;

### Examples
- `bot.exe -x 123 -y 456 -i image.png` - basic usage, `image.png` should be located in one folder with bot.
- `bot.exe --useMirror --imagePath http://imagehosting.example/image.png --leftX -123 -d --topY -456 --logFilePath D:\myLogs\bot.log`
- `bot.exe --notificationMode both --proxyAddress 1.2.3.4:5678 -i "relative path\with spaces\in double\quotes.png" --defenseMode --placingOrder left -x 123 -y 456 --disableUpdates`

### Notes:
- `--useMirror` and `--serverUrl` options are not compatible;
- Fully transparent parts of image are ignored.

## PixelPlanetWatcher
Program that logs updates in given rectangle to the binary file.

### Usage:
- `-l, --leftX` - **required**, X coordinate of left rectangle boundary;
- `-r, --rightX` - **required**, X coordinate of right rectangle boundary;
- `-t, --topY` - **required**, Y coordinate of top rectangle boundary;
- `-b, --bottomY` - **required**, Y coordinate of bottom rectangle boundary;
- `--useMirror` - if specified, changes base address to [fuckyouarkeros.fun](https://fuckyouarkeros.fun) (site mirror);
- `--serverUrl` - if specified, changes base address to your custom one - for those who deployed their own PixelPlanet copy;

### Notes:
- Changes are written to the file every minute.
- When closing with Ctrl+C, changes are also written to the file.
- DO NOT close app with `X` button if you do not want to lose pixels placed after last save.

## RecordVisualizer
Program that creates image sequence from files created by **Watcher**.

### Usage:
- `-f, --fileName` - **required**, path (relative/absolute) to file that is visualized;
- `--oldRecordFile` - enables old format mode (if file was recorded with version older than 2.0);
