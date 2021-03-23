# BreakIntoLines

## Description

This project is about a Java program that vectorizes a string into Java Path2D.Float paths, breaking it into lines and right justifying the text.

It started with a function in PostScript as shown in the project [𝝿 𝗩𝗲𝗰𝘁𝗼𝗿 𝗚𝗨𝗜 𝗳𝗼𝗿 𝗝𝗮𝘃𝗮 𝗮𝗻𝗱 𝗔𝗻𝗱𝗿𝗼𝗶𝗱](https://github.com/nilostolte/Projects-Presentations/blob/main/%CF%80%20Vector%20GUI%20for%20Java%20and%20Android.md#%CF%80-vector-gui-for-java-and-android). But PostScript was just a prototype language and it only takes Type 1 fonts where one cannot access Kerning Pairs because they are encrypted. With the project [𝗩𝗲𝗰𝘁𝗼𝗿 𝗙𝗼𝗻𝘁𝘀: 𝗜𝗻𝗳𝗼𝗿𝗺𝗮𝘁𝗶𝗼𝗻 𝗘𝘅𝘁𝗿𝗮𝗰𝘁𝗶𝗼𝗻 - 𝗚𝗹𝘆𝗽𝗵𝘀, 𝗧𝗵𝗲𝗶𝗿 𝗪𝗶𝗱𝘁𝗵𝘀 𝗮𝗻𝗱 𝗞𝗲𝗿𝗻𝗶𝗻𝗴 𝗣𝗮𝗶𝗿𝘀](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) one is able to read the Kerning Pairs as well as other font information directly from their font files. This is the final version which generates texts with Opentype and Truetype fonts without needing the original font files, which is appropriate to embedded applications.

After a font is converted with the 
[modified Glyph Inspector](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--major-breakthrough) that generates a font class that can be embedded into any 
Java program, the instance of this font class (they are singletons) is used to convert strings into paths. What it 
basically does is to search for the glyph in the font for each character in the string, to apply an appropriate 
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

## Method Description and Data Structures

### Decomposing Words

The initial text is a string that is to be converted to a formatted paragraph. The first step is to separate every word in the string through the method _split_ from class _String_. This method generates the array of strings `words` where each position contains a string with a word of the previous string. Next, the array `paragraph` of the same size is created but containing in each position a _Path2D.Float_ path with the glyphs of each character of each word as shown below:

![image](https://user-images.githubusercontent.com/80269251/112131564-0df32980-8ba0-11eb-8a24-894521243b42.png)

This process is done by searching each glyph in our embedded font (which is a Java class as explained in the project [**Automatic Vector Fonts Generator Project – Glyphs, their widths and kerning pairs**](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#font-transformed-in-a-java-class)). Each glyph of the font is defined as a Path2D.Float path, composed by commands `moveTo`, `lineTo`, `quadTo`, `curveTo`, and `closePath`, with the respective point coordinates. The glyphs are then traversed one by one, command by command, and their points are translated in x by the same amount for each glyph and scaled to the required size. For the first glyph the translation amount is zero, since it is assumed to be placed at the origin. Subsequent glyphs points are translated in x by the cumulated value of the previous characters widths and the kerning distances depending on the kerning pairs of characters in the word. Each point, once translated in x, will have both coordiantes multiplied by the scale factor. 

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

The following string was used to obtain the above result:

![image](https://user-images.githubusercontent.com/80269251/112013660-97531f00-8b00-11eb-9143-9bc29d31767c.png)



