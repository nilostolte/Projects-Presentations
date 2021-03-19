
![image](https://user-images.githubusercontent.com/80269251/111788201-2e686e80-8896-11eb-95f8-6bd6449abfbf.png)

#  π Vector GUI for Java and Android

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

As seen in https://github.com/nilostolte/Java-Vector-GUI/blob/main/MenuInfographics6/README.md#menuinfographics6, the **Java** class is used in a **Java** program. As shown in this program it is possible to insert additional information such as **TrueType** and **OpenType** fonts by reading these fonts with **Opentype.js** and transforming strings into path, since **PostScript** only processes **Type 1** and **Type 3** fonts. 

## Example 1: Menuinfographics6

![image](https://user-images.githubusercontent.com/80269251/111800784-accb0d80-88a2-11eb-876f-961e909ad3d9.png)

The code of this example can be found at:

https://github.com/nilostolte/Java-Vector-GUI/tree/main/MenuInfographics6

This example illustrates a semi-automatic approach where a menu has some elements developed in PostScript (including the original design, most texts and icons) and other elements written directly in Java (**Truetype** and **Opentype** fonts, programming, etc.)

Texts in PostScript make use of a homemade text justification and kerning functionality. Kerning is a typographical practice of spacing letters according to the visual effect to facilitate reading and is the subject of intense research in digital typography. This gives enormous potential not only when used in the system but also used independently, as for example, in an homemade automatic CV generator, parameterized with candidate information (my personal resume, entirely designed in PostScript, uses some of these functionalities).

This prototype is just a proof of concept and proves that we can easily generate Java code directly from the graphics design. It gives the opportunity to artists to program GUIs, leaving to the programmer the task of integrating it with the rest of the program. 
A more professional and finished product already developed and discussed later exploits information directly extracted from the font files. In this case any **Truetype** or **OpenType** font can be used without even having the font file in the system running the program. This allows using the technique in embedded applications, since the fonts or parts of them are embedded in the program. In these cases kerning is automatic because the kerning pairs table are imported from the font files directly in a outside program that does just that. This also streamlines the use of fonts because reading fonts and executing them are complex tasks and heavy code, consuming a lot of space and consuming considerable processing time. Our embedded fonts are already stored in the internal format that every vectorial shape is manipulated in Java. Also, these fonts are only used when unpredictable strings are needed as when the user types something. Fixed and short sized texts can be directly stored and executed in vectorized form without the need of passing through the intermediate string representation. Even though, our fonts are extremely streamlined, there is still some “interpretation” by the font to process the string and execute kerning, whereas in the vectorized form this interpretation has already taken place.


