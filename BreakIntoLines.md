# BreakIntoLines

## Description

This project is about a Java program that vectorizes a string into Java Path2D.Float paths, breaking it into lines and
right justifying the text.

After a font is converted with the 
[modified Glyph Inspector](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--major-breakthrough) that generates a font class that can be embedded into any 
Java program, the instance of this font class (they are singletons) is used to convert strings into paths. What it 
basically does is to search for the glyph in the font for each character in the string, to apply an apropriate 
translation and scale, and to write the path for the glyph. Before passing to the next character a variable holding 
the translation is incremented with the glyph width and with the kerning width for each pair of characters. Because of the
justification feature, kerning is only applied inside the words not between them. The space between the words is calculated by
the program to justify the text to the right.

For each line, when a certain line size is attained, the line is shown right justified and the y coordinate of the next line 
is incremented by a value passed as a parameter.

The program is able to handle 256 simultaneous fonts for each string. Each string becomes a new paragraph as described above. Font
switching is done by using character /000 followed by a character with the index of the font, that is, between /000 and /777 (255). 
These characters can appear at any place in a word, and they are not counted as actual characters.
Other non-printing characters can also be use as commands in this same manner.

## Examples

### With a Single Font
![image](https://user-images.githubusercontent.com/80269251/111925521-93cb8380-8a7f-11eb-94f8-d42d50366aa4.png)

In this snapshot it was used: a MyriadPro-Regular.otf font, scaled to 20 points size, line widths limited to 380 points, a
20 points y coordinate increment, and a 5 points minimum word separator.

### With Two Fonts

![image](https://user-images.githubusercontent.com/80269251/111985704-57ca0a00-8ae3-11eb-9e71-c319486bac6c.png)

In this snapshot it was used: MyriadPro-Regular.otf and MyriadPro-Bold.otf fonts, scaled to 20 points size, line widths 
limited to 380 points, a 20 points y coordinate increment, and a 4 points minimum word separator.

### With Four Fonts

![image](https://user-images.githubusercontent.com/80269251/112010236-8359ee00-8afd-11eb-817a-29a4984939ee.png)

In this snapshot it was used: MyriadPro-Regular.otf, MyriadPro-Bold.otf MyriadPro-It.otf and MyriadPro-SemiboldIt.otffonts, 
scaled to 20 points size, line widths limited to 380 points, a 20 points y coordinate increment, and a 4 points minimum word 
separator.
