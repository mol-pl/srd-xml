# School readers import

SRD stands for School Readers Data standard (schema).

The `srd.xsd` contains definition of XSD to be used for basic validation of readers data.

There are various tools (also online) that validate XML against XSD. One way is to use Netbeans IDE for that.

## Netbeans validation

1. Add attributes to a root element of a SRD file (so in DATA tag):
```
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="srd.xsd"
```

2. Open the SRD in Netbeans.

3. Run validation (via shortcut: ALT+SHIFT+F9; or choose from menu).

All errors will be shown below.

## VSC validation

Visual Studio Code is a free, light code editor with many extensions.

For XML/XSD validation you can use [Redhat XML extenstion](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml).

Once installed you just need schema location attributes added to a root element of your SRD file (same as for Netbeans).

The extension works live (continously). All invalid attributes should be underlined. They should also be shown in *Problems* panel.