## Problem

When some special UTF-8 characters inside a XML file, and your SAX’s parser is not configure to parse the UTF-8 properly, the following exception will be thrown.

    com.sun.org.apache.xerces.internal.impl.io.MalformedByteSequenceException:
    Invalid byte 1 of 1-byte UTF-8 sequence.
    ...

## Solution

The solution is quite simple, get the content in UTF-8 format, and override the SAX input source.

    File file = new File("c:\\file-utf.xml");
    InputStream inputStream= new FileInputStream(file);
    Reader reader = new InputStreamReader(inputStream,"UTF-8");

    InputSource is = new InputSource(reader);
    is.setEncoding("UTF-8");

    saxParser.parse(is, handler);

You can read the full example here – [how do read UTF-8 XML file with SAX parser](http://www.mkyong.com/java/how-to-read-utf-8-xml-file-in-java-sax-parser/)

[http://www.mkyong.com/java/sax-error-malformedbytesequenceexception-invalid-byte-1-of-1-byte-utf-8-sequence/](http://www.mkyong.com/java/sax-error-malformedbytesequenceexception-invalid-byte-1-of-1-byte-utf-8-sequence/)
