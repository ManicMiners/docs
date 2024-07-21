# DAT Section briefingsuccess

Similar to the briefing section, this section is text to be displayed to the user after they win and exit the map.

Generally the player would expect that this text would provide some sort of review of the map or maybe even information about the next mission if part of a campaign.

Each line of text is considered a paragraph, auto-wrapping to fit inside of the dialog box. Every line in this sections is part of the displayed text.

There is no known limit on the size of this section, the player is given a scrollable dialog box to read the text.

Use of the keyword `CADET` (upper case) will be automatically filled in with the players name when the dialog is displayed.

Example:

```
briefingsuccess{
CADET - you found the missing base, restored power to it and recovered all of the required crystals - job well done!

Use of the tunnel scout allowed you to quickly discover the caverns before they were filled with the rising lava.

Get some well deserved rest and prepare for your next away mission.
}
```

>The message may contain non-ANSI characters. If any are used, the editor will save the map using UTF16LE BOM format.