# Automatic Vector Fonts Generator Project – Glyphs, their widths and kerning pairs

This project started with the modification of the distances between certain pairs of characters, which is broadly known as kerning, of Type 1 
Fonts in PostScript. This was used to display right justified text using the function **BreakIntoLines**, a modified and enhanced version of a 
function with same name shown in the **PostScript Cookbook** (Blue Book) coded in PostScript. Postscript has been used as a prototype language to 
develop a much more complex project ([**π Vector GUI for Java and Android**](https://github.com/nilostolte/Projects-Presentations/blob/main/%CF%80%20Vector%20GUI%20for%20Java%20and%20Android.md#%CF%80-vector-gui-for-java-and-android)) which this project is part of.
 

The PostScript prototype has been used for different applications, but had quite a few inconveniences. First, 
the kerning had to be done by hand (the font kerning information is encrypted in the font and not available in PostScript). Second, this 
prototype cannot be used in another context (in a Java program, for example), except for showing static vectorized texts.  A vectorized 
text is a text represented by their graphical shapes, broadly called glyphs. A glyph is a series of commands to draw a character. Long 
vectorized texts are not a compact way to represent these texts because it will contain several repetitions of the same glyphs, thus wasting 
considerable space. It is neither not a convenient way to represent texts in a program, which is mainly done using sequences of character 
codes (ASCII or Unicode, for example), broadly called as strings. In text entered by the user, such as in a copy-paste context, for example, 
it is not possible to substitute the use of strings with their vectorized form. On the other hand, one cannot use PostScript to show messages 
in a program since PostScript interpreters are extremely complex and heavy.

The solution is to have fonts available to the program in order to show the glyphs corresponding to their characters. But, again, a font is an 
extremely complex file format that must be read in order to use its information. A program that reads fonts is called a parser, and a font parser 
is also a complex and heavy piece of software. Thus, it is far more convenient to use a font parser to extract the essential information and to 
generate a much more compact piece of code to make this information available to the program.


This is what has been accomplished in this project and what follows is a detailed description on how this has been accomplished. The essential 
information needed to display texts correctly on the screen using fonts is: the glyphs, their widths and the kerning pairs.

Besides glyphs and their widths, after several attempts to use font parsers in Java, a simple kerning pairs table could be acquired only for 
Truetype fonts. A more complete kerning pairs table may be supplied in the GPOS table, which is the only one available for Postscript fonts 
in Opentype font files. It is understandable that Adobe had done that to enhance the quality of their fonts. These fonts are generally also 
more compact and smoother because they use cubic Bezier curves instead of quadric Bezier curves used in Truetype. Fonts are a major business 
for Adobe and to guarantee that customers would continue to pay premium for them, they must make an extra effort in quality and in security 
to avoid copies. GPOS table is so complex to access and the documentation so scarce that even hackers get discouraged. 

With the need of fonts on the web, this table was cracked by Opentype.js, a very sophisticated and high level font parser. However, this has 
been an information mainly known by  Javascript and web programmers.

## Automatic Vector Fonts Generator Project – Major Breakthrough

A huge breakthrough has been acquired by using OpenType.js and the glyph inspector shown in the site https://opentype.js.org. This site provides
code to use OpenType.js in Javascript. The glyph inspector was modified and added the feature to generate a Java class with the essential 
information of the font.

![image](https://user-images.githubusercontent.com/80269251/111824482-a8abe980-88bc-11eb-91e2-d5b6ec839360.png)

## Error in Glyph Inspector

The only caveat found was that the code in this site had a bug. It was discovered that the function that returns 
the commands defining the glyphs were not being interpreted in the correct order when a set of points for cubic bezier curves are asked. This had 
been debugged using JSON.stringify that showed the correct order.

![image](https://user-images.githubusercontent.com/80269251/111824666-e14bc300-88bc-11eb-9a9a-a6f099a83d40.png)

## Font Transformed in a Java Class

This is how the embedded font looks like:
![image](https://user-images.githubusercontent.com/80269251/111825065-6800a000-88bd-11eb-98f8-0fd820fcb665.png)

