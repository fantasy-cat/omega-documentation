# launch

To launch Omega with custom flags, scroll to the bottom of the [sessions tab](https://constelia.ai/earth/dashboard/#sessions). You can add your custom launch arguments in `Launch Arguments`.

## --sync-logs
This will synchronize the `logger` module. 

By default, everything logged into console/terminal is asynchronous. Sometimes, the solution may crash and due to timing, the `logger` module will not display the closing error. Therefore, this setting will allow this to be synchronized. Though, you may notice a performance hit during launch.

## --verbose
This will display more details about certain logged messages. This isn't usually needed.

## --no-scripts
This will make Omega load with only the base scripts. This is useful for debugging.

## --ready-to-risk-it-all
Omega will continue to load despite anti-cheats installed. Risking your associated account, system, and other assets to be flagged for cheating or suspicious activity. Oddly, some members wish to be punished by third-party companies investigating them. This is a very dangerous option. Use at your own risk.

## --aim-only
Disables any ESP-related features. This is useful for those who only want to use aimbot and other aim-related features without any additional aid. This will disable any visuals, sounds, or other features that are related to ESP.

## --esp-only
Disables any aimbot-related features. Scripts cannot use any `input` related functions.