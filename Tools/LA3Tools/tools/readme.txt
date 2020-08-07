===============================================================
  Luminous Arc 3 Script Tools for character-pair font (v0.37)
===============================================================

Usage:
	"tool_name".exe <inputFile> <outputFile>

Processing steps:

--------------------
dumper.exe - text extractor
--------------------
- place here file with text to extract and rename it to "str.bin"
- run dumper.exe
- text should be extracted to new created "outOrg.txt" 

------------------
encoder.exe - character-pair font encoder
------------------
- place here translated "inT.txt" (Shift-JIS, Unix newline separator (0x0A)) 
- run encoder.exe
- "inTencoded.txt" will be created. (don't edit this file from this point, read only) 

------------------
strTabGen.exe - string table generator
------------------
- place "inTencoded.txt"
- run strTabGen.exe
- "strout.bin" will be created, replace in Tinke and check results.

-------
Tips
-------
- make sure "inTencoded.txt" and "outOrg.txt" have the same number of lines
- Recommended tool for edit - notepad++

--------
Notes
--------
- str*.bin is a string table binary structure of two strings (*char[2][])
  
  Textbox window allow to place:    

    in the first string of the structure element:
	- name of the character / box caption (no more than 12 halfsized letters)
    in the second string:
       - two lines of 20 Shift-JIS characters or 40 halfsized english characters 
       - box with the icon - you can place 16 Shift-JIS or 32 single chara-pairs

  str*.bin file has special script formatting codes:
    $n - new line
    $p - pause - awaits for button press( after that dialog box is cleaned )
    $e3 - option select (answer screen)
  
  You can place many textlines in one entry just place "$p" every next new line "$n"
  If 2nd string doesn't end with "$p" effect will be the same. (press button/pause)

  strsel.bin, strsana.bin (selection files) differ a bit:
  - first string is empty
  - second string sometimes contain symbol "-" 

  first line of extracted file *.txt is a textheader (16 bytes)
  
	
Available default font for character-pairs (80 characters) :

 !"#%&'()*+,-./:=?0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

-------------
changelog
-------------
v0.37
- removed whitespaces at the end of file, txt is now stream-friendly
- added that info to the textheader, code cleanup

v0.35
- added textheader (stores more or less important info from input binaries) 
- added batch-conversion directories pack (to work with big amount of files)
- added command line support for every script tools (it's backward compatible):
  Usage:
          "tool_name".exe <inputFile> <outputFile>

v0.31
- improved and simplified method of recognizing pointers in string table generator

v0.3
- str0.bin, strsel.bin, strana.bin files supported
- fixed method of recognizing pointers