# DAT Section briefingfailure

Similar to the briefingsuccess section, this section is text to be displayed to the user after they lose and exit the map.

Note that this is after the optional text the map may display to the player on why they lost the map due to lack of air, lack of miners/buildings, or by use of the `lose` event.

Generally the player would expect that this text would provide hints on how to complete the mission or maybe the consequences of the failure if part of a story-line.

Each line of text is considered a paragraph, auto-wrapping to fit inside of the dialog box. Every line in this section is part of the displayed text.

There is no known limit on the size of this section, the player is given a scrollable dialog box to read the text.

Use of the keyword `CADET` (upper case) will be automatically filled in with the players name when the dialog is displayed.

Example:

```
briefingfailure{
CADET - you failed to locate the missing base - wasting valuable resources and time.

Chief is disappointed in your performance and suggests defending your initial base better while quickly exploring more distant areas may help locate the missing base.

Review your plan and be ready to try again.
}
```

>The message may contain non-ANSI characters. If any are used, the editor will save the map using UTF16LE BOM format.