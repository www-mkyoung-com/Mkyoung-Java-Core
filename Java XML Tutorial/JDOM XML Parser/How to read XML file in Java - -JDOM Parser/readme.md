> JDOM is, quite simply, a Java representation of an XML document. JDOM provides a way to represent that document for easy and efficient reading, manipulation, and writing. It has a straightforward API, is a lightweight and fast, and is optimized for the Java programmer. It’s an alternative to DOM and SAX, although it integrates well with both DOM and SAX.

**JDOM**, Java XML parser, is more user friendly in the way of accessing the XML document.

In this example, we show you how to use JDOM to read a XML file, and print out each element orderly.

## 1\. Download the JDOM library

JDOM is not like SAX or DOM, which bundled in JDK. To use JDOM, you need to download the library manually.

Get JDOM from [JDOM official site ](http://www.jdom.org/downloads/source.html)or declares following dependency if you are using Maven.

    <dependency>
    <groupId>jdom</groupId>
    <artifactId>jdom</artifactId>
    <version>1.1</version>
        </dependency>

## 2\. XML File

XML file as following

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

## 3\. Java File

Use JDOM parser to parse above XML file.

    import java.io.File;
    import java.io.IOException;
    import java.util.List;
    import org.jdom.Document;
    import org.jdom.Element;
    import org.jdom.JDOMException;
    import org.jdom.input.SAXBuilder;

    public class ReadXMLFile {
    	public static void main(String[] args) {

    	  SAXBuilder builder = new SAXBuilder();
    	  File xmlFile = new File("c:\\file.xml");

    	  try {

    		Document document = (Document) builder.build(xmlFile);
    		Element rootNode = document.getRootElement();
    		List list = rootNode.getChildren("staff");

    		for (int i = 0; i < list.size(); i++) {

    		   Element node = (Element) list.get(i);

    		   System.out.println("First Name : " + node.getChildText("firstname"));
    		   System.out.println("Last Name : " + node.getChildText("lastname"));
    		   System.out.println("Nick Name : " + node.getChildText("nickname"));
    		   System.out.println("Salary : " + node.getChildText("salary"));

    		}

    	  } catch (IOException io) {
    		System.out.println(io.getMessage());
    	  } catch (JDOMException jdomex) {
    		System.out.println(jdomex.getMessage());
    	  }
    	}
    }

_Output_

    First Name : yong
    Last Name : mook kim
    Nick Name : mkyong
    Salary : 100000
    First Name : low
    Last Name : yin fong
    Nick Name : fong fong
    Salary : 200000

**Note**  
You may also at the following two examples :

*   [How to read XML file in Java – (SAX Parser)](http://www.mkyong.com/java/how-to-read-xml-file-in-java-sax-parser/)
*   [How to read XML file in Java – (DOM Parser)](http://www.mkyong.com/java/how-to-read-xml-file-in-java-dom-parser/)

[http://www.mkyong.com/java/how-to-read-xml-file-in-java-jdom-example/](http://www.mkyong.com/java/how-to-read-xml-file-in-java-jdom-example/)
