# BreakIntoLines Project

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

## Implementation Details and Data Structures

### Converting Strings to Glyphs

The initial text is a string that is to be converted to a formatted paragraph. The first step is to separate every word in the string through the method _split_ from class _String_. This method generates the array of strings `words` where each position contains a string with a word of the previous string. Next, the array `paragraph` of the same size is created but containing in each position a _Path2D.Float_ path with the glyphs of each character of each word as shown below:

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/112209967-7a961480-8bf0-11eb-8b85-aa1954d9e1ac.png" />
</p>

This process is done by searching each glyph in our embedded font (which is a Java class as explained in the project [**Automatic Vector Fonts Generator Project – Glyphs, their widths and kerning pairs**](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#font-transformed-in-a-java-class)). Each glyph of the font is defined as a Path2D.Float path, composed by `moveTo`, `lineTo`, `quadTo`, `curveTo`, or `closePath` segments, with their respective points coordinates. These coordinates are all defined in the font coordinate system where the contents are defined in <b><i>unitsPerEm</i></b>. A glyph is supposed to be a 1 point square, so its scale is <b><i>1÷unitsPerEm</i></b>. To scale glyphs to their proper size, coordinates must be multiplied by <b><i>(font size)÷unitsPerEm</i></b>.

Once the glyphs are searched, they are traversed one by one, segment by segment, and their coordinates are transformed accordingly. For the first glyph is not translated, since it is assumed to be placed at the origin. Subsequent glyphs x coordinates are incremented with the cumulated value of the previous glyphs and kerning widths, depending on their kerning pairs. Finally both coordinates are multiplied by the <b><i>scale</i></b> (_(font size)÷unitsPerEm_).

The resulting glyphs are stored in a _Path2D.Float_ path, as commented above. But a path cannot store a very important datum, which is the total word width, or in other words, the whole path width. That is why a new class `Word` is defined by inherinting it from _Path2D.Float_. The width of the path is then stored in the new class and instead of using a _Path2D.Float_ class one uses the `Word` class instead. Its definition in Java is as shown:

```
class Word extends Path2D.Float {
	double size;

	public void setWidth(double translation) { size = translation; }
	public double getWidth() { return size; }
}
```
The algorithm below details how the method is implemented. The _"input"_ `string` contains the characters of the word to be converted, and is actually a parameter passed to the method. The variable `word` is of type `Word`, inherited from _Path2D.Float_, the path created and being built in this method. At first, the x translation value `dx` is zero and the `word` path is created, being initially empty. Next, two loops are carried on. The first loop traverses all characters of `string`, one character at a time. For each character, the glyph path is searched in the font and saved in variable `p` of type _Path2D.Float_. The second loop traverses all segments of `p` until there are no more segments remaining. For each segment, the method tests if the segment is a `moveTo`, `lineTo`, `quadTo`, `curveTo`, or a `closePath`. Once the segment is identified, the points are translated and scaled as indicated, and a copy of the segment is appended to `word` by using its building segment methods `moveTo`, `lineTo`, `quadTo`, `curveTo`, and a `closePath` as indicated. Next, `dx` is incremented with the width of the glyph and with the kerning width, so the next glyph will be properly translated right after it. From there, the algorithm loops back to the test to see if path `p` is empty. 
Once it has no further segments, the width of the path (this is not indicated in the algorithm) is stored inside `word` in this way: `word.setWidth(dx * scale)`, and word is returned. 

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/112232446-f3a46480-8c0e-11eb-8fbb-e85edb303709.png" />
</p>

Notice that `dx` can be seen as a vector in the _font coordinate system_ because it is incremented with values (glyph widths and kerning widths) from the font which are also in the _font coordinate system_. That is why the scale must be applied to it, so it can be used in what can be seen as the _word, paragraph or line coordinate system_, since the three share the same coordinate system. When the line is finally _"shown"_ the words are finally transformed to the final _screen coordinate system_ when it can be explicitly _"seen"_. Implicitly, one is actually working with three different coordinate systems, although the transformation matrix is not necessary because calculations are very simplified, only involving scale and translations. 

A very important additional point one can easily see from what is shown here is that the result is always WYSIWYG, because "What You See" is exactly what is calculated internally, and it will remain unchanged in any other media. This is perhaps the most interesting reason to work with vector graphics primitives afterall.

### Breakintolines Method

#### The Algorithm

The algorithm for the <b><i>breakintolines</b></i> method is shown in the fluxogram below. The <b><i>input</b></i> is in reality the parameter to the method, that is the <b><i>paragraph</b></i> array containing the glyphs for each word as explained in the previous section. The <b><i>output</b></i> operator can be substituted by any output such as a file, a println, a display or a `Path.Float`. 
Each time a line is output the variable <b><i>yline</b></i> is incremented by <b><i>yinc</b></i>, the distance between the lines.

![image]()

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/112370456-cd84d000-8cb3-11eb-9074-52fa27ad72a3.png" />
</p>

#### Formatting the Paragraph

The process of formatting the paragraph is a matter of determining which words fit into a line. A line is limited in width and this is a parameter that should be provided (<b><i>pw</b></i> in the algorithm above). This will also determine the width of the paragraph formatted. As usual, this width is assumed to be in points (1/72 inch). A line is defined as an `ArrayList<Word>`, where words are 
stored one by one provided they all fit in the line, considering their widths and the space separating them. This space is calculated on the fly at each new word to be added. Once a word is unable to fit in the line anymore with the given constraints, the line is "shown" with the words separated by the calculated space (<b><i>ws</b></i> in the algorithm). 

#### _"Showing"_ the lines

Since each line is represented by a collection of words (actually an <b><i>ArrayList<Word></b></i>), each word assumed to be at the origin, the final line can be seen as a new path where the words are copied and translated according to their widths (see algorithm above) and the word separator <b><i>ws</b></i>. This final path is the actual line that can be either displayed, printed, or written to a file.

Subsequent lines are constructed in the same way, except that the y coordinates are incremented each time by <b><i>yinc</b></i>. The only differences between constructing lines and constructing words are that when constructing lines only translations are used (in words the glyphs were also scaled), words are separated by the calculated space <b><i>ws</b></i> (in words, glyphs were separated by the characters width and by kerning distances) and that y coordinates are incremented by <b><i>yinc</b></i> at each line (in words, y coordinates were scaled).

## Examples

### With a Single Font

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/111925521-93cb8380-8a7f-11eb-94f8-d42d50366aa4.png" />
</p>

In this snapshot it was used: a MyriadPro-Regular.otf font, scaled to 20 points size, line widths limited to 380 points, a
20 points y coordinate increment, and a 5 points minimum word separator.

### With Two Fonts

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/111985704-57ca0a00-8ae3-11eb-9e71-c319486bac6c.png" />
</p>

In this snapshot it was used: MyriadPro-Regular.otf and MyriadPro-Bold.otf fonts, scaled to 20 points size, line widths 
limited to 380 points, a 20 points y coordinate increment, and a 4 points minimum word separator.

### With Four Fonts

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/112010236-8359ee00-8afd-11eb-817a-29a4984939ee.png" />
</p>

In this snapshot it was used: MyriadPro-Regular.otf, MyriadPro-Bold.otf, MyriadPro-It.otf and MyriadPro-SemiboldIt.otf fonts, 
scaled to 20 points size, line widths limited to 380 points, a 20 points y coordinate increment, and a 4 points minimum word 
separator.

The following string was used to obtain the above result:

<p align="center"">
   <img src="https://user-images.githubusercontent.com/80269251/112013660-97531f00-8b00-11eb-9143-9bc29d31767c.png" />
</p>



