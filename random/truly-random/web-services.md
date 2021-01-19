---
description: Web applications
---

# Web services

### WSDL \(Web services description language\)

Describe web services \(location of service, methods, elements\) and written in XML.

It uses the following elements to describe the web service:

* `<types>` - datatype used by web service
* `<message>` - data definition and data elements for each operation
* `<portType>` - list of operations possible to perform and message involved
* `<binding>` - protocol & data format for each  port type

Example:

```text
// message element - define parts of each message and data type
<message name="getTagRequest">
    <part name="tag" type="xs:string"/>
    <part name="published" type="xs:string"/>
</message>

<message name="getTagResponse">
    <part name="value" type="xs:string"/>
</message>

// portType element - defines name of port and operation available
<portType name="glossaryTag"> // port name = glossaryTag
    <operation name="getTag"> // operation available = getTag
        <input message="getTagRequest"/> // operation has an input mesage (type defined above)
        <output message="getTagResponse"/> // operation has output message (defined above)
    </operation>
</portType>
```

### portType

* define a **web service**
* **operations** possible
* **message** involved in the operation

WSDL defines 4 different types of operation. Following are the list of operations:

1. **One-way** - operation can only receive the message \(no output\)
2. **Request-response** - operation can both receive and return a response
3. **Solicit-response** - operation can send a request and will wait for a response
4. **Notification** - operation can send a message but will not wait for a response



