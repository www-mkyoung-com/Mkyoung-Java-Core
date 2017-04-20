SAX parser is work differently with DOM parser, it does not load any XML document into memory and create some object representation of the XML document. Instead, the SAX parser use callback function (org.xml.sax.helpers.DefaultHandler) to informs clients of the XML document structure.

