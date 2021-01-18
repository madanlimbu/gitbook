# XML

### Intro

XML tags are not defined in any XML standard, they are defined by the author/developer of the XML document. 

Has tree structure, elements/tags can be root, parent, child, or siblings. All elements can have text content and attributes.

XML Prolog -  `<?xml version="1.0" encoding="UTF-8"?>` , specifies character encoding to avoid unique characters like international characters.

### Some chracterstics of XML:

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

### Namespaces

XML Namespaces help resolve the element name conflicts.

We can use prefix on element names to avoid the same name conflicts. However, a namespace for the prefix should be defined. 

`xmlns` attribute can be used to define a namespace. This can be declared in the attribute of the start tag of an element or on XML root element itself. 

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



