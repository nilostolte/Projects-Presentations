
#  π Vector GUI for Java and Android

![image](https://user-images.githubusercontent.com/80269251/111788201-2e686e80-8896-11eb-95f8-6bd6449abfbf.png)

Is a system for creating  Graphics User Interfaces (GUI) for Java applications on Windows, Linux or Android using vector primitives and vectorized fonts. Its goal is to help to create high quality and aesthetically attractive interfaces with the use of gradient effects and other vector graphics techniques (that previously could mostly be developed in programs such as Adobe Illustrator without the possibility of creating Java code) with high performance selection time, typically constant time for structured elements such as menus, grids, etc. Texts can use Truetype and Opentype fonts that are automatically transformed into Java through the a tool of the system (see project [𝗩𝗲𝗰𝘁𝗼𝗿 𝗙𝗼𝗻𝘁𝘀: 𝗜𝗻𝗳𝗼𝗿𝗺𝗮𝘁𝗶𝗼𝗻 𝗘𝘅𝘁𝗿𝗮𝗰𝘁𝗶𝗼𝗻 - 𝗚𝗹𝘆𝗽𝗵𝘀, 𝗧𝗵𝗲𝗶𝗿 𝗪𝗶𝗱𝘁𝗵𝘀 𝗮𝗻𝗱 𝗞𝗲𝗿𝗻𝗶𝗻𝗴 𝗣𝗮𝗶𝗿𝘀](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs)). Text can also be automatically formatted right justified by another tool of the system (see project [𝗕𝗿𝗲𝗮𝗸𝗜𝗻𝘁𝗼𝗟𝗶𝗻𝗲𝘀](https://github.com/nilostolte/Projects-Presentations/blob/main/BreakIntoLines.md#breakintolines)) allowing documentation to be shown as part of the interface or in heavily textual contents applications such as books or manuals. This makes it possible to design documents as interfaces to allow interactive books with no need of a browser, or any online content, ideal for embedded applications with real WYSIWYG contents.

It started with a prototype in PostScript and it has slowly been improved by transforming the prototype into a real system of tools written in Java. Nowadays the whole system uses Java for about 70% of the tasks (counting with examples, etc.), 20% of PostScript (mainly for icons, menus, etc. that are converted to Java semi automatically) and about 10% of JavaScript.

## Basic definitions

Definition of what vector graphics is and why this representation is better.  This concept is the main interest driving the use of vector graphics in GUIs. Zooming can become part of the interface and interactions can become more stimulating, more alive.

![image](https://user-images.githubusercontent.com/80269251/111790832-00385e00-8899-11eb-98bf-e307be744c40.png)

<br>

## Origins of the System

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/111805001-02a1b480-88a7-11eb-9df1-e8f411126d42.png">
</p>

This is the Maxcalc app that was once published in Google market. Some other apps were realized at that time such as a Sudoko game generator to play offline or to automatically solve a Sudoko grid offline. The creation of the popup menus and overall look of the design in MaxCalc (now called π calculator) is the original idea of the system. 

By looking in more detail the design of interfaces using vector primitives I have realized that these primitives inherited their basic elements from their distant cousins, the vector graphics languages that I already knew and had already more than 30 years of experience. To link these two worlds together a proof should be shown that this would really work. The starting linking element was the Java and Android Java “path” primitive where the placement of several vector primitives together give origin to more complex graphics elements. With the hands on a graphics element in PostScript and a digit in a vector font, both transformed into Java paths and displayed into an Android application is sufficient proof that this is feasible.

## Prototype: Semi-automatic GUI generation system

<br>

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127531622-464d50fa-fc48-4338-98f5-25bd0a068ac2.png">
</p>

The diagram shows the data flow between each element of the <b>system prototype</b>. Starting from an initial file with the vector information of a drawing in **PostScript**, **PDF**, **Ai** (**Adobe Illustrator** format, which is, in fact, a **PDF** file or a **PostScript** file) or **SVG** which was produced in a software (**Adobe Illustrator**, **Inkscape**, etc.) or written directly in **PostScript**. This file was originally created by an artist (graphic designer) or homemade. In the first case, the examples implemented here were retrieved free of charge from the Internet (mainly from **Freepik**).
This file is then converted to **PostScript**. If the file was originally designed in **PostScript** it must also sometimes be converted into a **PostScript** file with only pure graphics, that is to say, devoid of any programming element since **PostScript** is also a programming language (moreover this feature is fully exploited in this system). This is achieved by various tools, such as: **Ghostview** (it is the workhorse in this system, which is a free **PostScript** interpreter for **Windows** or **Unix**), **Acrobat Pro** (software from **Adobe**, the creator of **PostScript** and **PDF**, capable of reading **PostScript** and **PDF** files and transforming them from one format to another or into other formats), **Illustrator ** (product of  **Adobe**, very expensive graphics designer professional tool, and inaccessible to non-graphic designer users) and **Inkscape** (free software for generating and converting **SVG** files to other formats). Other tools are possible. These are just few examples.

Then this file is restructured **by hand** through a text editor (**Notepad++**) so as to facilitate the automatic generation of a **Java** class and enriched with functions previously designed for this and other purposes, such as **kerning, texts justification, manipulation of strings** and other very important functions. The resulting file can be set to either be viewed by **PostScript** viewer (**Ghostview**, **Acrobat Pro**, etc.) or to generate the **Java** class, which is the result of our system. First the file is viewed in **PostScript** for correction of visual errors and then converted to **Java**. Each time the **Java** class is changed, this **PostScript** file must be modified because the **Java** class is generated automatically. 

In [MenuInfographics6](https://github.com/nilostolte/Java-Vector-GUI/blob/main/MenuInfographics6/README.md#menuinfographics6), pieces of the design are automatically generated, and integrated in a Java program. The program was completely written in Java except for all the vector information. As shown in this program it is possible to insert additional information such as **TrueType** and **OpenType** fonts by [reading these fonts with **Opentype.js**](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) and [transforming strings into path](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project), since **PostScript** only processes **Type 1** and **Type 3** fonts. 

## Example 1: Menuinfographics6

### Screenshot and Code

Click [here](https://github.com/nilostolte/Java-Vector-GUI/tree/main/MenuInfographics6#screenshot) for a more recent screenshot of this example.

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127532961-1c02deaa-15c0-4636-aa7c-644a327a4cbb.png">
</p>

Please check the [code](https://github.com/nilostolte/Java-Vector-GUI/tree/main/MenuInfographics6) for this example.

### Description

This example illustrates a semi-automatic approach where a menu has some elements developed in PostScript (including the original design, items descriptions texts and icons, as illustrated [here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)), other elements written directly in Java (gradients, programming, etc.), and other elements using [this program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) (to read **Truetype** and **Opentype** fonts) and [this program](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) (to convert strings into `Path2d.Float`).

### Automatic Kerning Information and Embeddedable Fonts

Texts in PostScript make use of a homemade text justification and kerning functionality. Kerning is a typographical practice of spacing letters according to the visual effect to facilitate reading and is the subject of intense research in digital typography. This gives enormous potential not only when used in the system but also used independently, as for example, in an homemade automatic CV generator, parameterized with candidate information (my personal resume, entirely designed in PostScript, uses some of these functionalities).

The initial prototype is just a proof of concept and proves that we can easily generate Java code directly from the graphics design. It gives the opportunity to artists to program GUIs, leaving to the programmer the task of integrating it with the rest of the program. 
As mentioned earlier, a more professional and finished [product](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) already developed and further discussed below exploits glyphs, their widths and kerning information directly extracted from the font files. In this case one can use any **Truetype** or **OpenType** font without even having the font file in the system running the program. This allows using the technique in embedded applications, since the fonts or parts of them are embedded in the program. In these cases kerning is automatic because the kerning pairs table are imported from the font files directly in a outside program that does just that. This also streamlines the use of fonts because reading fonts and executing them are complex tasks and heavy code, consuming a lot of space and consuming considerable processing time. Our embedded fonts are already stored in the internal format that every vectorial shape is manipulated in Java. Also, these fonts are only used when unpredictable strings are needed as when the user types something. Fixed and short sized texts can be directly stored and executed in vectorized form without the need of passing through the intermediate string representation. Even though, our fonts are extremely streamlined, there is still some “interpretation” by the font to process the string and execute kerning, whereas in the vectorized form this interpretation has already taken place.

## Exemple 2
<br>

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127533566-98610102-61c0-4106-be99-58b4da0d1ce6.png">
</p>

In this example the entire Java class was originally programmed in PostScript and automatically generated by the system ([as illustrated here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)), even the function of selecting menu items (item 3 is being selected in the screenshot). This type of operation is simply done with a Java code cartouche inside the PostScript code ([as illustrated here](https://github.com/nilostolte/PostScript/tree/main/Examples/Convertion%20to%20Java/ExclamationIcon#exclamationicon)). The advantage here is the considerable reduction in development time because 100% of the programming elements are written in advance and contain no errors.
According to the article below, _"cartouches help to decouple the interwoven design and engineering concerns"_. Although here we use a simple form of cartouche, its effect is visibly beneficial in the overall method. It is rather intuitive that decoupling releases complexity from the whole process. By the way, **decoupling and information hiding are also key elements in objet oriented design**. Also of note, in the article below they also used similar aspects of our methodology, particularly the use of vector graphics representation which is somehow translated (they use external parsing while we "parse" directly in PostScript) into a program in a language such as Java.

* please see  [**"Cartouche: Conventions for Tangibles Bridging Diverse Interactive Systems"**](https://www.cct.lsu.edu/~corntoole/papers/ullmer-tei10-cartouche.pdf), Brygg Ulmer et al. TEI 2010, January 24-26, 2010, Cambridge, Massachusetts, USA. ACM Classification keywords: H.5.2: User Interfaces (D.2.2, H.1.2, I.3.6)

We continue using this methodology without using Postscript. Since this system in PostScript is just a working and useful **prototype** and it has a number of pitfalls (the lack of transparency being the most flagrant), we continue generating Java code with Java as well as with Javascript in the final implementation. Languages are just tools chosen for their convenience. Java as our goal language is also used for convenience because of its portability in several machines and operating systems. The system is a set of tools in diverse languages to preprocess the information and isolate the implementation details from the program to concentrate in the essential.


## Justification and Kerning Functionalities

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127534381-2d491b09-42b6-41da-ac6f-9d9ff694c59b.png">
</p>

On the right is a part of the program containing the **BreakIntoLines** function which justifies the text as indicated by the GhostView window on the left. This function was inspired by the function of the same name given in **"PostScript Cookbook"** (also known as the "bluebook") which makes the distribution of a text in multiple lines, but which has been generalized with right justification and kerning implementations. Some software, such as **Illustrator**, have these functions but they are carefully hidden and transparent to the user. However, **kerning algorithms** are not too advanced depending on the software and the worst part is that they cannot be enhanced or modified. For example, it is possible to use **PowerPoint** to format a text and then use it in our system, but the quality of kerning leaves much to be desired in some cases. Our **kerning** is based purely on the visual appearance of two neighboring letters and it requires doing it **by hand**. This is an advantage but it has an enormous inconvenient: it is very time consuming. Once determined, these measures will not change for a given font. In addition, luckily, this method can use the majority of measures from another similar-looking font. For example, all **Sans Serif** fonts (currently very fashionable) are very similar and share a majority of measures. In these cases only a handful of measures need to be changed from a font to another.

However, this **kerning** method is only interesting for short texts to be used artistically. For heavy usage, with a huge variety of fonts, as it is usually the case in real life, this is not practical. For this reason another [program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) has been developed for the final system, replacing the prototype, that reads **Truetype** and **Opentype** fonts directly from their files. This [program](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs) reads the kerning pairs information given by the font designer. This information is then used in our embedded font methodology to display the text the way it was intended by the font designer. Another [program](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project) was developed to vectorize strings into Java Path2D.Float paths. These two programs are able to process more heavy duty tasks for any kind of font, but just for titles and text not justified. For justified text as in case of booklets, brochures or other longuer and formatted texts, another [**BreakIntoLines**](https://github.com/nilostolte/Projects-Presentations/blob/main/BreakIntoLines.md#breakintolines) was developed in Java to substitute the function with the same name in the prototype.


# New Java Tools in the System to Substitute the Prototype

## Updated Data Flow Diagram
<br>

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127383023-08b64f0a-7ea9-4d1b-b539-4f6129597d4e.png">
</p>

<br>

## Automatic Vector Fonts Generator Project – Glyphs, their widths and kerning pairs

Please check this [link to the project](https://github.com/nilostolte/Projects-Presentations/blob/main/Automatic%20Vector%20Fonts%20Generator%20Project.md#automatic-vector-fonts-generator-project--glyphs-their-widths-and-kerning-pairs).

The project started changing the distances between pairs of characters (**kerning**) of **Type 1 Fonts** in **PostScript** to display right 
justified text in PostScript that has been used as a prototype language.

The prototype had quite a few flaws. First, the kerning was done by hand (kerning information is encrypted in the font and not available in PostScript). Second, it cannot be used in another context (in a Java program, for example), except for showing static vectorized texts; i.e., when each character appears as a graphical shape (a glyph: a series of commands to draw a character), since PostScript interpreters are complex and heavy and can't be used in a Java program. In addition, a long vectorized text is not compact since it contains repetitions of the same glyphs. Also, programs rather use strings (sequences of character ASCII or Unicode codes). In error messages, for example, it is hard to predict every error, including system ones, to swap strings for their vectorized form. The solution is to have fonts in the program. But a font is an extremely complex file format. A font parser (a program that reads fonts) is also a complex and heavy piece of software. What has been done in this project is to use a font parser to read the font file outside the program and to copy the information in the program.

Font parsers in Java supply access to Glyphs, their widths, and a simple kerning pairs table but only for Truetype fonts, not for Postscript fonts in Opentype. Adobe has opted to supply a better but much more complex table for better quality for their fonts that are also more compact and smoother for using cubic instead of quadric Bezier curves.

A huge breakthrough was using OpenType.js and the glyph inspector of the site https://opentype.js.org, which was modified to generate a Java class for the font. A caveat was a bug that didn't take the correct order of points for bezier curves from the function returning glyph commands, which was debugged with JSON.stringify.

## String Vectorizer Project

Please check this [link to the project](https://github.com/nilostolte/Projects-Presentations/blob/main/String%20Vectorizer.md#string-vectorizer-project).

This project is about a program that vectorizes strings into Java Path2D.Float paths.

## BreakIntoLines Project

This [project](https://github.com/nilostolte/Projects-Presentations/blob/main/BreakIntoLines.md#breakintolines) is about a 
Java program that vectorizes a string into Java Path2D.Float paths, breaking it into lines and right justifying the text.

## BreakIntoLines in PDFBox: Creating Multipage Formatted Documentation in PDF

The Apache PDFBox library is an open source Java tool for working with PDF documents. The Apache PDFBox
library project allows viewing PDF documents, creation of new PDF documents, manipulation of existing
documents and the ability to extract content from documents. Apache PDFBox also includes several
command-line utilities.
In this project, PDFBox was added the capability to format text coming from a stream (only a file or a string at
the moment, but it can be easily extended to other sources). It is a custom stream that is actually implemented
by a generic interface for reading words from a text source.
Two classes were created for different purposes: BreakIntoLines and BreakIntoDocLines. The first allows to
format paragraphs into a PDF page and the other generates an entire PDF formatted file as an electronic book
with several pages.
The choice here was to use the standard embedded fonts instead of displaying the glyphs ourselves from a
custom dictionary. This is done for improved fonts antialiasing when shown on the screen. This is because in
our system the glyphs are shown with standard antialiasing on the screen but hints embedded in the fonts to
simplify the display when the scale is very small are not used to save space and to ease implementation.
The major goal of this project is to supply a way to generate online documentation that is also printable in PDF
format. The same text can be used to be displayed online or in PDF format with identical format (WYSIWYG).

The example below shows two formatted paragraphs in PDF with different fonts. Two examples are introduced in PDFBox
to show the features proposed: **ShowJustifiedFormattedText.java** and **ShowJustifiedFormattedBook.java**.
The first example is the one shown below. PDFBox has several examples that help users to use the various
features this software offers.

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127384737-ed6d0d48-eff0-485f-b2b4-2ef039a4e83c.png">
</p>

Below, an example of book copied from a web site using a Java program to quickly jump to the text and copy
just the book. The PDF book generated is shown using the PDF Debugger from PDFBox. On the right, the code
of the first page of the file is shown just opening the “Page: 1” tag and clicking on “Contents”.

![image](https://user-images.githubusercontent.com/80269251/127379206-3f21c948-e03c-4c8b-82a9-367c606465e6.png)

Detail of the PDF code generated. Notice the font switching (/F1, /F2, /F3 and /F4) and the two bytes characters to avoid encoding vector. Characters are indexed directly by their Glyph Index (GID). Compression greatly reduces the space due redundancy. Notice the transformation matrix at the beginning of each line.

<p align="center">
  <img src="https://user-images.githubusercontent.com/80269251/127379359-0704f50b-ddfe-4999-a376-03647d0e7bf8.png">
</p>

Please check [this link](https://github.com/nilostolte/PDFBox#running-the-pdf-viewer) for a discussion on how to use PDF Debugger, a space analysis between the standard procedure to justify text in PDF in comparison with our method, different problems concerning space savings (particularly by using Td command instead of a transformation matrix), a comparison between different embeddable fonts in PDFBox, as well as a discussion about compression.

## Converting  Java Vector to PowerPoint With FreeHEP: MicroVBA

MicroVBA is our VBA interpreter written in VBA to be used in PowerPoint in order to be able to import large vector graphics files.

In this project, the Java vector information shown on the screen, such as a Graphics User interface, is automatically converted to PowerPoint by using an intermediate language, MicroVBA. The information is written in a file containing the MicroVBA instructions that are read within a macro in the PowerPoint file where the vector information is created in our MicroVBA interpreter by executing the instructions. MicroVBA is a subset of VBA for PowerPoint. This language bypasses the weaknesses of the EMF format (the lack of gradient being the most handicapping) and of VBA itself (limitations on the size of functions) in order to import complete vector files from Java programs to PowerPoint.

The program that transforms the Java information to MicroVBA is a modification of FreeHEP library. As mentioned in Part 1, it uses an independent graphics superclass that writes the MicroVBA instructions into a file. The user triggers the conversion by clicking on a bar on the top of the screen. 

A PowerPoint presentation that mocks the converted interface representing [this menu](https://github.com/nilostolte/Java-Vector-GUI/tree/main/MenuInfographics6) can be found [here](https://github.com/nilostolte/MicroVBA-PowerPoint/blob/main/Example/testfontsembedded.pptm) and the instructions how to set and build it are given [here](https://github.com/nilostolte/MicroVBA-PowerPoint/tree/main/Example).

Clicking an option in the menu will make a frame appear. These are Powerpoint frames not part of the original Java menu on the left. This presentation is ideal to show how the menu works in Java. It behaves exactly in the same way. As indicated there, when an element is clicked instead of activating the real activity in the real Java program, this mockup just shows an explanation on what the real Java program does. This is not only good as a didactical tool, but also as a tool for documentation. When an element is clicked it flashes to show this menu element has been clicked, exactly as it does in the original menu in Java. Next, an animation is triggered with a new frame with the explanation. The animation is actually done by a macro that makes the previous frame disappear and the new frame appear. The texts in the menus are copied to the presentation as vector paths, not as text, and they look exactly as in Java. This is how they are represented in the original Java program. They are transferred to the presentation via a MicroVBA file that is generated in the application totally automatically. The interpreter is necessary because the file is large.

# Conclusion: Graphics Designers as GUI Creators - a less expensive and superior way to create GUIs

Because of the clutter, the design difficulty and lack of elegance and flexibility of available elements for creating interfaces on **Android**, the need of richer graphics designs for **Java Android** has been first detected. The difficulty perceived was that the design, the colors and art are of an extreme importance for the appearance of a graphics interface element. However, these elements are, in general, designed by programmers and not by artists. Realizing that this has been a huge mistake for decennials and that only now artists start to express themselves in web sites design, it is logical to think to use some of these very modern and evolved resources also in the universe of interfaces for Android applications.

This is a great opportunity for enterprises to save a lot in software development, since interfaces are very important for the look and feel of the program. This is so wide known that many sci-fi movies show computer programs only through fancy manipulations of a graphics user interface. One of the first movies to exploit zooming in computer interfaces was in **Blade Runner**. 

Since skilled programmers are very expensive, it is far better to let them take care of more complex parts of a program, and leave the design to graphics designers artists. With proper tools, such as **Adobe XD**, interactive interfaces can be created by graphics designers. The vector design as well as the interactive events defined in Adobe XD can be read and transformed in Java code implementing this design. One blatant advantage of this approach is that making deep changes in the interface is easy, fast and bug-free, since its code is generated automatically. Prototyping with several entirely different versions of the same interface gives birth to a whole new way of developing programs.
