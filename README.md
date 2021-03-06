word2docbook
============

Convert Word documents (docx) to XML docbook 5.0, usign XSLT 2.0 with [saxonhe9-2-1-5j](http://saxon.sourceforge.net/) and XMLPipeline with [calumet](https://community.emc.com/docs/DOC-4242).

This converter makes the transformation based on a file which makes a relationship between word styles and docbook tags.

The output will has this form:
```xml
<book xmlns="http://docbook.org/ns/docbook" version="5.0">
    <info>
    </info>
     <chapter xml:id="m0">
        <info></info>
     </chapter>
     <chapter xml:id="m1">
        <info></info>
     </chapter>
     <chapter xml:id="m2">
        <info></info>
     </chapter>
     ...
</book>
```

Elements supported:
 table in cals mode
 listitem
 emphasis
 links
 sect1..5
 chapter
 book
 mediaobject
 important
 blockquote
 mathml
 info
 title
 preface
 authorgroup
 author
 personblurb
 footnotes

##Installation

Download de code.
Install java 1.6.

##Usage

Execute word2docbook.bat wordfile, without extension.
The process will take the document from the input folder and store it in the output folder in xml docbook format.

In the template folder there is a file with the conversion instructions: template.xml.

```xml
<t:template xmlns:t="http://www.omaonk.com/schema">
   <t:style word="heading 1" tag="chapter"/> <!-- title word style -->
   <t:style word="heading 2" tag="sect1"/> <!-- title 1 -->
   <t:style word="heading 3" tag="sect2"/> <!-- title 2 -->
   <t:style word="List Paragraph" tag="listitem"/>
   <t:style word="heading 4" tag="sect3"/> <!-- title 3 -->
   <t:style word="heading 5" tag="sect4"/> <!-- title 4 -->
   <t:style word="heading 6" tag="example"/>
   <t:style word="Quote" tag="blockquote"/>
   <t:style word="Intense Quote" tag="important"/>
   <t:style word="Title" tag="title"/>
   <t:style word="Author" tag="author"/>
   <t:style word="personblurb" tag="personblurb"/>
</t:template>
```
In this file you can find the rules conversions, for example if the docx document contains a heading 1 style, this is transformed to chapter. Tables, lists and inline elements (bold, underline, sub, sup, links, ...) are autodetected.

Its important to mark, in the docx, the title, heading 1, heading 2,..., because this marks are used to generate de XML docbook structure, you can use the template/template.xml template sample.

The main XSL file is: word2docbook.xsl and you can change the input parameters:

path.unzip.word = temporal folder
template.estils = template path

```xml
<xsl:param name="path.unzip.word" select="'C:/word2docbook/tmp'"/>
<xsl:param name="template.estils" select="'C:/word2docbook/templates/template.xml'"/>
<xsl:param name="codi"/>
<xsl:param name="titol"/>
```
##Styling word document 

Steps to mark word documents:
1) Open MicrosoftOficce Word and load a document.
1) Mark the document title, you have to apply the style title (in the microsoft office editor) to the document title.
2) Create sections:
  - Use title1, title2, title3, title4,... Word style to create the document structure, each of this styles will be transformed to chapter, sect1, sect2, sect3,...
  - Preface section is a title1 Style with the 'Preface' literal.

3) You can modify the template.xml file and apply diferent style that will be tansformed to docbook tags. For example (default template):
    - Quote will be converted to blockquote
    - Intense Quote will be converted to important.
4) Save as docx.


##Demo

1)In the input folder there is a test.docx document, this document is a simple document with sections, paragraphs, tables, bold, italic, images, equations and list items.
Execute: word2docbook.bat test
The output will be in the output folder in XML docbook format and with the document images.

2)Sample 2: test_2.docx word with preface, author, personalblurb and footnotes.
