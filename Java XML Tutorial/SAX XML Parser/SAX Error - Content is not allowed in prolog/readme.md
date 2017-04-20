## Problem

Working XML via SAX parser, but when it parse some XML file, it prompts following error message :

    org.xml.sax.SAXParseException: Content is not allowed in prolog.
    	at org.apache.xerces.util.ErrorHandlerWrapper.createSAXParseException(Unknown Source)
    	at org.apache.xerces.util.ErrorHandlerWrapper.fatalError(Unknown Source)
    	at org.apache.xerces.impl.XMLErrorReporter.reportError(Unknown Source)
    	//...

## Solution

This error message is always caused by the invalid XML content in the beginning element. For example, extra small dot “.” in the beginning of XML element.

Any characters before the “**<?xml….**” will cause above “**org.xml.sax.SAXParseException: Content is not allowed in prolog**” error message.

A small dot “.” before the “<?xml….

    .<?xml version="1.0"?>
    <company>
    	<staff>
    		<firstname>yong</firstname>
    		<lastname>mook kim</lastname>
    		<nickname>mkyong</nickname>
    		<salary>100000</salary>
    	</staff>
    	<staff>
    		<firstname>low</firstname>
    		<lastname>yin fong</lastname>
    		<nickname>fong fong</nickname>
    		<salary>200000</salary>
    	</staff>
    </company>

To fix it, just delete all those weird characters before the “**<?xml**“.
[http://www.mkyong.com/java/sax-error-content-is-not-allowed-in-prolog/](http://www.mkyong.com/java/sax-error-content-is-not-allowed-in-prolog/)
