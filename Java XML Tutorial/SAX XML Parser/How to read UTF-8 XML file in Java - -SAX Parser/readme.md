In previous [Java SAX XML example](http://www.mkyong.com/java/how-to-read-xml-file-in-java-sax-parser/), there is no problem if you use SAX to parse a plain text (ANSI) XML file, however, if you parse a XML file which contains some special UTF-8 characters, it will prompts “[Invalid byte 1 of 1-byte UTF-8 sequence](http://www.mkyong.com/java/sax-error-malformedbytesequenceexception-invalid-byte-1-of-1-byte-utf-8-sequence/)” exception.

    com.sun.org.apache.xerces.internal.impl.io.MalformedByteSequenceException:
    Invalid byte 1 of 1-byte UTF-8 sequence.

See following xml file which contain a special UTF-8 characters “§” (press [Alt + 789](http://tools.oratory.com/altcodes.html))

    <?xml version="1.0"?>
    <company>
    	<staff>
    		<firstname>yong</firstname>
    		<lastname>mook kim</lastname>
    		<nickname>§</nickname>
    		<salary>100000</salary>
    	</staff>
    </company>

To fix it, just override the SAX input source like this :

    File file = new File("c:\\file-utf.xml");
    InputStream inputStream= new FileInputStream(file);
    Reader reader = new InputStreamReader(inputStream,"UTF-8");

    InputSource is = new InputSource(reader);
    is.setEncoding("UTF-8");

    saxParser.parse(is, handler);

See a full example of using SAX parser to parse a Unicode XML file.

    package com.mkyong.test;

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.Reader;
    import javax.xml.parsers.SAXParser;
    import javax.xml.parsers.SAXParserFactory;
    import org.xml.sax.Attributes;
    import org.xml.sax.InputSource;
    import org.xml.sax.SAXException;
    import org.xml.sax.helpers.DefaultHandler;

    public class ReadXMLUTF8FileSAX
    {
        public static void main( String[] args )
        {
        	try {

        	      SAXParserFactory factory = SAXParserFactory.newInstance();
        	      SAXParser saxParser = factory.newSAXParser();

        	      DefaultHandler handler = new DefaultHandler() {

        	        boolean bfname = false;
        	        boolean blname = false;
        	        boolean bnname = false;
        	        boolean bsalary = false;

        	        public void startElement(String uri, String localName,
        	            String qName, Attributes attributes)
        	            throws SAXException {

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
        	                String qName)
        	                throws SAXException {

        	              System.out.println("End Element :" + qName);

        	        }

        	        public void characters(char ch[], int start, int length)
        	            throws SAXException {

        	          System.out.println(new String(ch, start, length));

        	          if (bfname) {
        	            System.out.println("First Name : "
        	                + new String(ch, start, length));
        	            bfname = false;
        	          }

        	          if (blname) {
        	              System.out.println("Last Name : "
        	                  + new String(ch, start, length));
        	              blname = false;
        	           }

        	          if (bnname) {
        	              System.out.println("Nick Name : "
        	                  + new String(ch, start, length));
        	              bnname = false;
        	           }

        	          if (bsalary) {
        	              System.out.println("Salary : "
        	                  + new String(ch, start, length));
        	              bsalary = false;
        	           }

        	        }

        	      };

        	      File file = new File("c:\\file.xml");
        	      InputStream inputStream= new FileInputStream(file);
        	      Reader reader = new InputStreamReader(inputStream,"UTF-8");

        	      InputSource is = new InputSource(reader);
        	      is.setEncoding("UTF-8");

        	      saxParser.parse(is, handler);

        	    } catch (Exception e) {
        	      e.printStackTrace();
        	    }

        }
    }

[http://www.mkyong.com/java/how-to-read-utf-8-xml-file-in-java-sax-parser/](http://www.mkyong.com/java/how-to-read-utf-8-xml-file-in-java-sax-parser/)
