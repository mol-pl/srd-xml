# School readers import

***SRD*** stands for ***School Readers Data*** standard (schema).

The standard can be used for data exchange between programs. In particular for importing school readers to library management systems like LibraNET or MOL NET+.

How to create an SRD file
-------------------------

Ideally an SRD file would be generated via some software. It is a text file so you can view it in almost any editor, but creating it by hand might be complicated. So the SRD file should be created with an automatic export or a script.  

Note that by *SRD file* we mean an XML file that was created in accordance with the SRD standard. You can use `srd` extension for your files (e.g. `pupils.srd`). Just like in the examples. 

What is in the file
-------------------

An SRD file is mainly for students (pupils), but can also contain data of teachers etc. So for all readers in a library.

### Basic structure of the XML ###
* The root of XML is the `DATA` element (tag). The tag can contain attributes for validation. See e.g. `examples/pupils.srd`.
* You should add a `SOURCE` element on top to provide meta-data of the source program.
* Base element with data is a `STUDENT` element (also used for pupils).
* You can optionally use `OTHER` to also import teachers and other stuff members.

By design readers can be of any nationality. So in examples you will see various national letters (e.g. Czech "ř", Polish "ś"). That is why you *SHOULD* use UTF-8 as an encoding of your file. 

### Basic requirements ###
* Any reader *MUST* have a first and a last name.
* Readers uniqueness *SHOULD* be recognised with a combination of fields: first name, last name, national ID.
* For students school ID and class ID (grade) *SHOULD* also be taken into account for uniqueness.

So to add a reader with the same first and a last name you have to add a national ID. But also students with the same first and a last name can be in different classes/grades (or in different schools).  

### National ID ###
* NID for Poland is the PESEL.
* NID for USA is the Social Security Number.
* NID can be skipped especially for countries that don't use it (e.g. UK).

### Notes ###
* You can find more notes in the XSD file (in `xs:documentation` tags). 
* Some fields *MIGHT* have other requirements depending on specific needs of a program or a library (institution).
* The destination program *SHOULD* check it's own specific requirements (not only validate with XSD).
* For example `barcode` *MIGHT* need to be unique for a whole library. Also checked with records added earlier.
* Some fields *MIGHT* have special meaning for example `email` might be used both for identification (auth) and for contacting readers (notifications). 
* Some fields *MIGHT* also need to be of specific length.

Validation
----------

The `srd.xsd` contains definition of XSD to be used for basic validation of readers data.

There are various tools (also on-line) that validate XML against XSD. One way is to use Netbeans IDE for that. Below we also provide instructions for a smaller editor - Visual Studio Code (VSC).

### Netbeans validation ###

[Netbeans](https://netbeans.apache.org/) is a free, large program for developers (IDE).

1. Add attributes to a root element of a SRD file (so in DATA tag):
```
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="srd.xsd"
```

2. Open the SRD in Netbeans.

3. Run validation (via shortcut: ALT+SHIFT+F9; or choose from menu).

All errors will be shown below.

### VSC validation ###

[Visual Studio Code](https://code.visualstudio.com/) is a free, lightweight code editor with many extensions.

For XML/XSD validation you can use [Redhat XML extenstion](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml).

Once installed you just need schema location attributes added to a root element of your SRD file (same as for Netbeans).

The extension works live (continuously). All invalid attributes should be underlined. They should also be shown in *Problems* panel.
