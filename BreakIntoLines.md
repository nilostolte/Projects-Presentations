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

The program is able to handle 8 simultaneous fonts for each string. Each string becomes a new paragraph as described above. Font
switching is done by using characters /000 to /007 acting each one as an index to a different font. These characters can appear
at the beginning of words to appear with the particular fonts indexed by them, and they are not counted as actual characters.
Other non-printing characters can also be use as commands in this same manner.

## Snapshot with a Single Font
![image](https://user-images.githubusercontent.com/80269251/111925521-93cb8380-8a7f-11eb-94f8-d42d50366aa4.png)

