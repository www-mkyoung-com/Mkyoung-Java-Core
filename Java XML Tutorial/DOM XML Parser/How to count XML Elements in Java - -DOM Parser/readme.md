In this example, we show you how to use **DOM Parser** to count the total number of elements in a XML file. First, search the element name, and then you can use `NodeList.getLength()` to get the total number of available elements.

    NodeList list = doc.getElementsByTagName("staff");
    System.out.println("Total of elements : " + list.getLength());

_File : file.xml_

    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <company>
    	<staff id="1">
    		<firstname>yong</firstname>
    		<lastname>mook kim</lastname>
    		<nickname>mkyong</nickname>
    		<salary>2000000</salary>
    		<age>29</age>
    	</staff>
    	<staff id="2">
    		<firstname>low</firstname>
    		<lastname>yin fong</lastname>
    		<nickname>fong fong</nickname>
    		<salary>1000000</salary>
    	</staff>
    	<staff id="3">
    		<firstname>Ali</firstname>
    		<lastname>Baba</lastname>
    		<nickname>Alibaba</nickname>
    		<salary>199000</salary>
    		<age>40</age>
    	</staff>
    </company>

_File : CountXMLElement.java_ – Search total number of available “**staff**” elements.

    import java.io.IOException;
    import javax.xml.parsers.DocumentBuilder;
    import javax.xml.parsers.DocumentBuilderFactory;
    import javax.xml.parsers.ParserConfigurationException;
    import org.w3c.dom.Document;
    import org.w3c.dom.NodeList;
    import org.xml.sax.SAXException;

    public class CountXMLElement {

      public static void main(String argv[]) {

    	try {
    		String filepath = "c:\\file.xml";
    		DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
    		DocumentBuilder docBuilder = docFactory.newDocumentBuilder();
    		Document doc = docBuilder.parse(filepath);

    		NodeList list = doc.getElementsByTagName("staff");

    		System.out.println("Total of elements : " + list.getLength());

    	} catch (ParserConfigurationException pce) {
    		pce.printStackTrace();
    	} catch (IOException ioe) {
    		ioe.printStackTrace();
    	} catch (SAXException sae) {
    		sae.printStackTrace();
    	}
      }
    }

Output

    Total of elements : 3

[http://www.mkyong.com/java/how-to-count-xml-elements-in-java-dom-parser/](http://www.mkyong.com/java/how-to-count-xml-elements-in-java-dom-parser/)
