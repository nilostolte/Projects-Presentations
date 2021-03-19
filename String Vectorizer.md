# String Vectorizer Project

This project, also known as **VectFontStr2Path2D**, is about a program that vectorizes strings into Java `Path2D.Float` paths. After a
font is converted with the modified [Glyph Inspector](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--major-breakthrough)
that generates a font class that can be embedded into any Java program, the instance of this class font (they are singletons) is used to convert strings 
into paths. What it basically does is to search for the glyph in the font for each character in the strings, to apply an apropriate translation and scale, 
and to write the path for the glyph. Before passing to the next character a variable holding the translation is incremented with the glyph width and 
with the kerning width for each pair of characters.
