# DAT file format

## Physical format
The physical format is mainly of interest to those creating .DAT files outside of the Manic Mainer editor.  For the purposes of this document, the terms ANSI is referring to characters up to 0x7F. Characters 0x80 and higher are non-ANSI.

The DAT file is a text file organized into sections. Every line in the map file ends in the Windows CRLF combination (carriage-return line-feed). The text reading logic of the Manic Miner engine supports the following formats:

- ANSI 8 bit (Windows current code page) with no BOM.
- UTF8 with BOM - (byte 1: 0xef, byte 2: 0xbb, byte 3:0xbf)
- UTF16LE with BOM. (byte 1: 0xff, byte 2: 0xfe)
- UTF16BE with BOM. (byte 1: 0xfe, byte 2: 0xff)

BOM is short for `B`yte `O`rder `M`arker. This is an optional sequence of bytes at the beginning of a UTF file that are defined in the UTF spec. If you are reading/writing .DAT files with your own code, you need to support these.

> 8 bit files without a BOM are treated by the engine as windows current code page. Depending on the non-ANSI text in the file, it is possible for windows current code page to not match UTF8 encoding.  If your utility is going to save non-ANSI text into the .DAT file - your utility should save using UTF8 BOM or UTF16LE BOM format to avoid any incorrect translations.

>UTF16 formats without BOM (both little endian and big endian) are NOT supported by Manic Miners. If using UTF16 the file must have a BOM.

>UTF32 formats (both little endian and big endian, with and without BOM) are NOT supported by Manic Miners. If you are editing on a Mac make sure your text files are not in UTF32 format.

The Windows end of text file character CTRL-Z (26) is not required at the end of the .DAT file and should not be included. If it is included, it must be the last character of the file.

The Manic Miner editor may create UTF16LE BOM or ANSI no BOM formats. Testing has shown that use of non-ANSI characters is one way that the engine will save the map in UTF16LE BOM format. It is unknown what other decisions the editor makes to decide what encoding to write a new map.

## Internationalization

While the map engine does read in UTF16 and UTF8 formats, the engine does not generally support internationalization. All sections names must be in lower case ANSI western (a-z). Variable names and Event Chain names in script must be in ANSI western (A-Z, a-z, 0-9).

Internationalized strings appear to work correctly in the info section for levelname and creator, inside script strings, and for the text contained within the three briefing sections. Use of non-ANSI characters will automatically cause Manic Miners to save using UTF16LE BOM format.

## Sections

The map editor built into Manic Miners will rewrite the .DAT file on every save. The file is organized into sections, and the editor will write every section even if it is empty. During map read, the order is not important, however the editor will always write the sections in the following order below.

A section starts with one of the below names, followed by the open braces character `{`. The section ends when a single close braces character is on its own line `}`. Every line of text in-between the open and close braces characters is treated as data for that section.  Every section has its own specific format for the lines that make up that section.

Following is the order of sections written by map editor. Click each section for detailed information about that section.

1. [comments](_pages/DATSectioncomments)
2. [info](_pages/DATSectioninfo)
3. [tiles](_pages/DATSectiontiles)
4. [height](_pages/DATSectionheight)
5. [resources](_pages/DATSectionresources)
6. [objectives](_pages/DATSectionobjectives)
7. [buildings](_pages/DATSectionbuildings)
8. [landslidefrequency](_pages/DATSectionlandslidefrequency)
9. [lavaspread](_pages/DATSectionlavaspread)
10. [miners](_pages/DATSectionminers)
11. [briefing](_pages/DATSectionbriefing)
12. [briefingsuccess](_pages/DATSectionbriefingsuccess)
13. [briefingfailure](_pages/DATSectionbriefingfailure)
14. [vehicles](_pages/DATSectionvehicles)
15. [creatures](_pages/DATSectioncreatures)
16. [blocks](_pages/DATSectionblocks)
17. [script](_pages/ScriptingStructure)

There are two legacy sections that are still accepted but completely ignored. They are no longer generated or needed by the editor.
- monsters
- monsterfrequency

Example of an empty section:
```mms
comments{
}
```
