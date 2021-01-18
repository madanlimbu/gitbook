# XML

### Intro

XML tags are not defined in any XML standard, they are defined by the author/developer of the XML document. 

Has tree structure, elements/tags can be root, parent, child, or siblings. All elements can have text content and attributes.

XML Prolog -  `<?xml version="1.0" encoding="UTF-8"?>` , specifies character encoding to avoid unique characters like international characters.

### Some characterIstics of XML:

* Must have a closing tag
  * We can however use a self-closing tag for empty elements - `<title />` 
  * _Note: empty elements can still have attributes_
* Tags are case sensitive
* Attribute values must be quoted - `<title lang="en">example</title>` 
* Certain characters should be replaced with safe characters.
  * Character like `<` will result in an error as the parser interprets it as the start of a new element
  * To avoid these error, there are replacement safe value chracter \(Entity references\), which are given below:
    * `&lt;` = `<` less than
    * `&gt;` = `>` greater than
    * `&amp;` = `&` ampersand
    * `&apos;` = `'` apostrophe
    * `&quot;` = `"` quotation mark
* white space is preserved - no truncation for multiple white-spaces
* `<!-- can be used for comment -->` but no double dashes allow in middle `like -- this` 
* Newlines are stored as `LF` 
  * For reference on how OS stores newlines them \(Carriage return & line feed\):
    * Windows - `CR + LF` 
    * Unix & Mac OSX - `LF` 
    * Old mac - `CR` 
    * XML - `LF` 
* Elements naming rules:
  * must start with a letter or underscore \(except letters `xml` \)
  * case-sensitive
  * can contain letters, digits, hyphens, underscores, and periods
  * cannot contain spaces

> **Tip:** An entity has three parts: it starts with an ampersand \(&\), then comes the entity name, and it ends with a semicolon \(;\).

### Namespaces

XML Namespaces help resolve the element name conflicts.

We can use prefix on element names to avoid the same name conflicts. However, a namespace for the prefix should be defined. 

`xmlns` attribute can be used to define a namespace. This can be declared in the attribute of the start tag of an element or on the XML root element itself. 

The namespace declaration has syntax `xmlns:prefix="URI"` .

```text
<root xmlns:customprefix="http://www.test.com">
...
</root>

or 

<customprefix:image xmlns:customprefix="http://www.test.com">
    <customprefix:title>example 2</customprefix:title>
</customprefix:image>
```

Note: the URI will not be used by the parser to look up information but to give namespace a unique name. However, it is a good practice to have URI to a page explaining the namespace information for developers.

**Default namespace** - We can also define a default namespace for an element to avoid using prefixes in all of its child elements. syntax = `xmlns="namespaceURI"` example:

```text
<image xmlns="http://www.test.com">
    <title>example 2</title>
</image>
```

### XML Validation

There are two terms used in XML Validation:

1. "well formed" - A XML document with correct syntax
2. "valid" - A XML document that is  "well formed" XML document and validated against a _**document type definition**_

> **Document type definition \(Schema of XML\)** - defines the rules, structure, standard, and allowed elements and attributes for an XML Document.

There is two document type definition that can be used with XML:

1. [DTD ](https://www.w3schools.com/xml/xml_dtd.asp)- The original Document Type Definition
2. [XML Schema](https://www.w3schools.com/xml/xml_schema.asp) - An XML-based alternative to DTD



