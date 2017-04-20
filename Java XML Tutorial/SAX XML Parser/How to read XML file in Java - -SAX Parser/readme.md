**SAX parser** is working differently with a DOM parser, it neither load any XML document into memory nor create any object representation of the XML document. Instead, the SAX parser use callback function (`org.xml.sax.helpers.DefaultHandler`) to informs clients of the XML document structure.

    SAX Parser is faster and uses less memory than DOM parser.

See following SAX callback methods :

*   **startDocument()** and **endDocument()** – Method called at the start and end of an XML document.
*   **startElement()** and **endElement()** – Method called at the start and end of a document element.
*   **characters()** – Method called with the text contents in between the start and end tags of an XML document element.

## 1\. XML file

Create a simple XML file.

    <?xml version="1.0"?>
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

## 2\. Java file

Use SAX parser to parse the XML file.

    import javax.xml.parsers.SAXParser;
    import javax.xml.parsers.SAXParserFactory;
    import org.xml.sax.Attributes;
    import org.xml.sax.SAXException;
    import org.xml.sax.helpers.DefaultHandler;

    public class ReadXMLFile {

       public static void main(String argv[]) {

        try {

    	SAXParserFactory factory = SAXParserFactory.newInstance();
    	SAXParser saxParser = factory.newSAXParser();

    	DefaultHandler handler = new DefaultHandler() {

    	boolean bfname = false;
    	boolean blname = false;
    	boolean bnname = false;
    	boolean bsalary = false;

    	public void startElement(String uri, String localName,String qName,
                    Attributes attributes) throws SAXException {

    		System.out.println("Start Element :" + qName);

    		if (qName.equalsIgnoreCase("FIRSTNAME")) {
    			bfname = true;
    		}

    		if (qName.equalsIgnoreCase("LASTNAME")) {
    			blname = true;
    		}

    		if (qName.equalsIgnoreCase("NICKNAME")) {
    			bnname = true;
    		}

    		if (qName.equalsIgnoreCase("SALARY")) {
    			bsalary = true;
    		}

    	}

    	public void endElement(String uri, String localName,
    		String qName) throws SAXException {

    		System.out.println("End Element :" + qName);

    	}

    	public void characters(char ch[], int start, int length) throws SAXException {

    		if (bfname) {
    			System.out.println("First Name : " + new String(ch, start, length));
    			bfname = false;
    		}

    		if (blname) {
    			System.out.println("Last Name : " + new String(ch, start, length));
    			blname = false;
    		}

    		if (bnname) {
    			System.out.println("Nick Name : " + new String(ch, start, length));
    			bnname = false;
    		}

    		if (bsalary) {
    			System.out.println("Salary : " + new String(ch, start, length));
    			bsalary = false;
    		}

    	}

         };

           saxParser.parse("c:\\file.xml", handler);

         } catch (Exception e) {
           e.printStackTrace();
         }

       }

    }

_Result_

    Start Element :company
    Start Element :staff
    Start Element :firstname
    First Name : yong
    End Element :firstname
    Start Element :lastname
    Last Name : mook kim
    End Element :lastname
    Start Element :nickname
    Nick Name : mkyong
    End Element :nickname
    Start Element :salary
    Salary : 100000
    End Element :salary
    End Element :staff
    Start Element :staff
    Start Element :firstname
    First Name : low
    End Element :firstname
    Start Element :lastname
    Last Name : yin fong
    End Element :lastname
    Start Element :nickname
    Nick Name : fong fong
    End Element :nickname
    Start Element :salary
    Salary : 200000
    End Element :salary
    End Element :staff
    End Element :company

**Warning**  
This example may encounter exceptions for **UTF-8** XML file, please read this article about [how to read the XML “UTF-8” file in SAX](http://www.mkyong.com/java/how-to-read-utf-8-xml-file-in-java-sax-parser/)

**Note**  
You may interest to read this [How to read XML file in Java – (DOM Parser)](http://www.mkyong.com/java/how-to-read-xml-file-in-java-dom-parser)

[http://www.mkyong.com/java/how-to-read-xml-file-in-java-sax-parser/](http://www.mkyong.com/java/how-to-read-xml-file-in-java-sax-parser/)
