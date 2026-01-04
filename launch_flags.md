# launch

To launch Omega with custom flags, there are two options:

- Open terminal/console, and launch the `.bat` and pass the flags alongside. (`omega.bat --sync-logs`). On Linux, opening `omega.sh` is implied to be completed in terminal. You should always launch it through the terminal on Linux.

- You can edit the `.bat` or `.sh` and change the launch arguments to your liking.

## --sessions
This is the same as `--session`. This will validate your Session or create a new one if it doesn't exist. By default, Omega always launches with this flag through the `.bat` or `.sh` file. 

There isn't really a reason to remove this flag.

## --sessions-only
This is the same as `--session-only`. This will validate or create a new Session like usually when launching with `--sessions`. However, this will not launch the solution after. 

This is usually for reading the terminal/console buffer of Omega. In the case you are working on an ecosystem project that reads the output from Omega, this is helpful.

## --sync-logs
This will synchronize the `logger` module. 

By default, everything logged into console/terminal is asynchronous. Sometimes, the solution may crash and due to timing, the `logger` module will not display the closing error. Therefore, this setting will allow this to be synchronized. Though, you may notice a performance hit during launch.

## --verbose
This will display more details about certain logged messages. This isn't usually needed.

## --no-scripts
This will make Omega load with only the base scripts. This is useful for debugging.

## --ready-to-risk-it-all
Omega will continue to load despite anti-cheats installed. Risking your associated account, system, and other assets to be flagged for cheating or suspicious activity. Oddly, some members wish to be punished by third-party companies investigating them. This is a very dangerous option. Use at your own risk.