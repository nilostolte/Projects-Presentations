
#  π Vector GUI for Java and Android

![image](https://user-images.githubusercontent.com/80269251/111788201-2e686e80-8896-11eb-95f8-6bd6449abfbf.png)

Is a system for creating  Graphics User Interfaces (GUI) for Java applications on Windows, Linux or Android using vector primitives and vectorized fonts.

## Basic definitions

Definition of what vector graphics is and why this representation is better.  This concept is the main interest driving the use of vector graphics in GUIs. Zooming can become part of the interface and interactions can become more stimulating, more alive.

![image](https://user-images.githubusercontent.com/80269251/111790832-00385e00-8899-11eb-98bf-e307be744c40.png)

<br>

## Prototype: Semi-automatic GUI generation system

<br>

![image](https://user-images.githubusercontent.com/80269251/111790751-e9920700-8898-11eb-91a4-ff6ba61c2e52.png)


The diagram shows the data flow between each element of the <b>system prototype</b>. Starting from an initial file with the vector information of a drawing in **PostScript**, **PDF**, **Ai** (**Adobe Illustrator** format, which is, in fact, a **PDF** file or a **PostScript** file) or **SVG** which was produced in a software (**Adobe Illustrator**, **Inkscape**, etc.) or written directly in **PostScript**. This file was originally created by an artist (graphic designer) or homemade. In the first case, the examples implemented here were retrieved free of charge from the Internet (mainly from **Freepik**).
This file is then converted to **PostScript**. If the file was originally designed in **PostScript** it must also sometimes be converted into a **PostScript** file with only pure graphics, that is to say, devoid of any programming element since **PostScript** is also a programming language (moreover this feature is fully exploited in this system). This is achieved by various tools, such as: **Ghostview** (it is the workhorse in this system, which is a free **PostScript** interpreter for **Windows** or **Unix**), **Acrobat Pro** (software from **Adobe**, the creator of **PostScript** and **PDF**, capable of reading **PostScript** and **PDF** files and transforming them from one format to another or into other formats), **Illustrator ** (product of  **Adobe**, very expensive graphics designer professional tool, and inaccessible to non-graphic designer users) and **Inkscape** (free software for generating and converting **SVG** files to other formats). Other tools are possible. These are just few examples.

Then this file is restructured **by hand** through a text editor (**Notepad++**) so as to facilitate the automatic generation of a **Java** class and enriched with functions previously designed for this and other purposes, such as **kerning, texts justification, manipulation of strings** and other very important functions. The resulting file can be set to either be viewed by **PostScript** viewer (**Ghostview**, **Acrobat Pro**, etc.) or to generate the **Java** class, which is the result of our system. First the file is viewed in **PostScript** for correction of visual errors and then converted to **Java**. Each time the **Java** class is changed, this **PostScript** file must be modified because the **Java** class is generated automatically. 

In [MenuInfographics6](https://github.com/nilostolte/Java-Vector-GUI/blob/main/MenuInfographics6/README.md#menuinfographics6), pieces of the design are automatically generated, and integrated in a Java program. The program was completely written in Java except for all the vector information. As shown in this program it is possible to insert additional information such as **TrueType** and **OpenType** fonts by [reading these fonts with **Opentype.js**](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) and [transforming strings into path](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project), since **PostScript** only processes **Type 1** and **Type 3** fonts. 

## Example 1: Menuinfographics6

![image](https://user-images.githubusercontent.com/80269251/111800784-accb0d80-88a2-11eb-876f-961e909ad3d9.png)

Please check the [code](https://github.com/nilostolte/Java-Vector-GUI/tree/main/MenuInfographics6) for this example.

This example illustrates a semi-automatic approach where a menu has some elements developed in PostScript (including the original design, items descriptions texts and icons, as illustrated [here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)), other elements written directly in Java (gradients, programming, etc.), and other elements using [this program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) (to read **Truetype** and **Opentype** fonts) and [this program](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) (to convert strings into `Path2d.Float`).

Texts in PostScript make use of a homemade text justification and kerning functionality. Kerning is a typographical practice of spacing letters according to the visual effect to facilitate reading and is the subject of intense research in digital typography. This gives enormous potential not only when used in the system but also used independently, as for example, in an homemade automatic CV generator, parameterized with candidate information (my personal resume, entirely designed in PostScript, uses some of these functionalities).

This prototype is just a proof of concept and proves that we can easily generate Java code directly from the graphics design. It gives the opportunity to artists to program GUIs, leaving to the programmer the task of integrating it with the rest of the program. 
As mentioned earlier, a more professional and finished [product](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) already developed and further discussed below exploits information directly extracted from the font files. In this case any **Truetype** or **OpenType** font can be used without even having the font file in the system running the program. This allows using the technique in embedded applications, since the fonts or parts of them are embedded in the program. In these cases kerning is automatic because the kerning pairs table are imported from the font files directly in a outside program that does just that. This also streamlines the use of fonts because reading fonts and executing them are complex tasks and heavy code, consuming a lot of space and consuming considerable processing time. Our embedded fonts are already stored in the internal format that every vectorial shape is manipulated in Java. Also, these fonts are only used when unpredictable strings are needed as when the user types something. Fixed and short sized texts can be directly stored and executed in vectorized form without the need of passing through the intermediate string representation. Even though, our fonts are extremely streamlined, there is still some “interpretation” by the font to process the string and execute kerning, whereas in the vectorized form this interpretation has already taken place.

## Exemple 2

![image](https://user-images.githubusercontent.com/80269251/111802041-efd9b080-88a3-11eb-879e-39297c5d5c58.png)

In this example the entire Java class was originally programmed in PostScript and automatically generated by the system ([as illustrated here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)), even the function of selecting menu items (item 3 is being selected in the screenshot). This type of operation is simply done with a Java code cartouche inside the PostScript code ([as illustrated here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)). The advantage here is the considerable reduction in development time because 100% of the programming elements are written in advance and contain no errors.
According to the article below, _"cartouches help to decouple the interwoven design and engineering concerns"_. Although here we use a simple form of cartouche, its effect is visibly beneficial in the overall method. It is rather intuitive that decoupling releases complexity from the whole process. By the way, **decoupling and information hiding are also key elements in objet oriented design**. Also of note, in the article below they also used similar aspects of our methodology, particularly the use of vector graphics representation which is somehow translated (they use external parsing while we "parse" directly in PostScript) into a program in a language such as Java.

* please see  [**"Cartouche: Conventions for Tangibles Bridging Diverse Interactive Systems"**](https://www.cct.lsu.edu/~corntoole/papers/ullmer-tei10-cartouche.pdf), Brygg Ulmer et al. TEI 2010, January 24-26, 2010, Cambridge, Massachusetts, USA. ACM Classification keywords: H.5.2: User Interfaces (D.2.2, H.1.2, I.3.6)

We continue using this methodology without using Postscript. Since this system in PostScript is just a working and useful **prototype** and it has a number of pitfalls (the lack of transparency being the most flagrant), we continue generating Java code with Java as well as with Javascript in the final implementation. Languages are just tools chosen for their convenience. Java as our goal language is also used for convenience because of its portability in several machines and operating systems. The system is a set of tools in diverse languages to preprocess the information and isolate the implementation details from the program to concentrate in the essential.


## Justification and Kerning Functionalities

![image](https://user-images.githubusercontent.com/80269251/111804723-b787a180-88a6-11eb-96a0-25e05d849f72.png)

On the right is a part of the program containing the **BreakIntoLines** function which justifies the text as indicated by the GhostView window on the left. This function was inspired by the function of the same name given in **"PostScript Cookbook"** (also known as the "bluebook") which makes the distribution of a text in multiple lines, but which has been generalized with right justification and kerning implementations. Some software, such as **Illustrator**, have these functions but they are carefully hidden and transparent to the user. However, **kerning algorithms** are not too advanced depending on the software and the worst part is that they cannot be enhanced or modified. For example, it is possible to use **PowerPoint** to format a text and then use it in our system, but the quality of kerning leaves much to be desired in some cases. Our **kerning** is based purely on the visual appearance of two neighboring letters and it requires doing it **by hand**. This is an advantage but it has an enormous inconvenient: it is very time consuming. Once determined, these measures will not change for a given font. In addition, luckily, this method can use the majority of measures from another similar-looking font. For example, all **Sans Serif** fonts (currently very fashionable) are very similar and share a majority of measures. In these cases only a handful of measures need to be changed from a font to another.

However, this **kerning** method is only interesting for short texts to be used artistically. For heavy usage, with a huge variety of fonts, as it is usually the case in real life, this is not practical. For this reason another [program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) has been developed for the final system, replacing the prototype, that reads **Truetype** and **Opentype** fonts directly from their files. This [program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) reads the kerning pairs information given by the font designer. This information is then used in our embedded font methodology to display the text the way it was intended by the font designer. Another [program](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) was developed to vectorize strings into Java Path2D.Float paths. These two 
programs are able to process more heavy duty tasks for any kind of font, but without text justification yet.

## Origins of the System

![image](https://user-images.githubusercontent.com/80269251/111805001-02a1b480-88a7-11eb-9df1-e8f411126d42.png)

This is the Maxcalc app that was once published in Google market. Some other apps were realized at that time such as a Sudoko game generator to play offline or to automatically solve a Sudoko grid offline. The creation of the popup menus and overall look of the design in MaxCalc (now called π calculator) is the original idea of the system. 

By looking in more detail the design of interfaces using vector primitives I have realized that these primitives inherited their basic elements from their distant cousins, the vector graphics languages that I already knew and had already more than 30 years of experience. To link these two worlds together a proof should be shown that this would really work. The starting linking element was the Java and Android Java “path” primitive where the placement of several vector primitives together give origin to more complex graphics elements. With the hands on a graphics element in PostScript and a digit in a vector font, both transformed into Java paths and displayed into an Android application is sufficient proof that this is feasible.

# Graphics Designers as GUI Creators: a less expensive and superior way to create GUIs

Because of the clutter, the design difficulty and lack of elegance and flexibility of available elements for creating interfaces on **Android**, the need of richer graphics designs for **Java Android** has been first detected. The difficulty perceived was that the design, the colors and art are of an extreme importance for the appearance of a graphics interface element. However, these elements are, in general, designed by programmers and not by artists. Realizing that this has been a huge mistake for decennials and that only now artists start to express themselves in web sites design, it is logical to think to use some of these very modern and evolved resources also in the universe of interfaces for Android applications.

This is a great opportunity for enterprises to save a lot in software development, since interfaces are very important for the look and feel of the program. This is so wide known that many sci-fi movies show computer programs only through fancy manipulations of a graphics user interface. One of the first movies to exploit zooming in computer interfaces was in **Blade Runner**. 

Since skilled programmers are very expensive, it is far better to let them take care of more complex parts of a program, and leave the design to graphics designers artists. With proper tools, such as **Adobe XD**, interactive interfaces can be created by graphics designers. The vector design as well as the interactive events defined in Adobe XD can be read and transformed in Java code implementing this design. One blatant advantage of this approach is that making deep changes in the interface is easy, fast and bug-free, since its code is generated automatically. Prototyping with several entirely different versions of the same interface gives birth to a whole new way of developing programs.

# Automatic Vector Fonts Generator Project – Glyphs, their widths and kerning pairs

Please check this [link to the project](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs).

The project started changing the distances between pairs of characters (**kerning**) of **Type 1 Fonts** in **PostScript** to display right 
justified text in PostScript that has been used as a prototype language.

The prototype had quite a few flaws. First, the kerning was done by hand (kerning information is encrypted in the font and not available in PostScript). Second, it cannot be used in another context (in a Java program, for example), except for showing static vectorized texts; i.e., when each character appears as a graphical shape (a glyph: a series of commands to draw a character), since PostScript interpreters are complex and heavy and can't be used in a Java program. In addition, a long vectorized text is not compact since it contains repetitions of the same glyphs. Also, programs rather use strings (sequences of character ASCII or Unicode codes). In error messages, for example, it is hard to predict every error, including system ones, to swap strings for their vectorized form. The solution is to have fonts in the program. But a font is an extremely complex file format. A font parser (a program that reads fonts) is also a complex and heavy piece of software. What has been done in this project is to use a font parser to read the font file outside the program and to copy the information in the program.

Font parsers in Java supply access to Glyphs, their widths, and a simple kerning pairs table but only for Truetype fonts, not for Postscript fonts in Opentype. Adobe has opted to supply a better but much more complex table for better quality for their fonts that are also more compact and smoother for using cubic instead of quadric Bezier curves.

A huge breakthrough was using OpenType.js and the glyph inspector of the site https://opentype.js.org, which was modified to generate a Java class for the font. A caveat was a bug that didn't take the correct order of points for bezier curves from the function returning glyph commands, which was debugged with JSON.stringify.

# String Vectorizer Project

Please check this [link to the project](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project).

This project is about a program that vectorizes strings into Java Path2D.Float paths.
